---
title: Fetching Data In React | The Odin Project
source: https://www.theodinproject.com/lessons/node-path-react-new-fetching-data-in-react
author: 
published: 
created: 2024-12-08
description: The Odin Project empowers aspiring web developers to learn together for free
tags:
  - coding
---
## Using fetch in React components

Now, let’s take a look at how we can incorporate `fetch` into a similar React component. One common use case is to fetch data from an API when a component mounts, so that the data can be displayed on screen.

Whenever a component needs to make a request as it renders, it’s often best to wrap that `fetch` inside of an effect.

```jsx
import { useEffect, useState } from "react";

const Image = () => {
  const [imageURL, setImageURL] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
      .then((response) => response.json())
      .then((response) => setImageURL(response[0].url))
      .catch((error) => console.error(error));
  }, []);

  return (
    imageURL && (
      <>
        <h1>An image</h1>
        <img src={imageURL} alt={"placeholder text"} />
      </>
    )
  );
};

export default Image;
```

`useState` lets us add the `imageURL` state, whereas `useEffect` allows us to perform side effects. In this case, the side effect is fetching data from an external API. Since we need to fetch the data only once when the component mounts, we pass an empty dependency array.

### Handling errors

Working over the network is inherently unreliable. The API you’re making a request to might be down, there could be network connectivity issues, or the response you receive could contain errors. A multitude of things can go wrong, and if you don’t preemptively plan for errors, your website can break or appear unresponsive to users.

To simulate a network error, scroll up to the previous code snippet and change the `fetch` URL to something random. After a refresh of your browser window, the page will remain a blank white screen, without giving the user any indication that the page has finished loading or that there was an error.

To fix this, we need to check for *something* before Image component returns JSX. We’ll call it: `error`.

```jsx
if (error) return <p>A network error was encountered</p>

return (
  imageURL && (
    <>
      <h1>An image</h1>
      <img src={imageURL} alt={"placeholder text"} />
    </>
  )
);
```

To set this `error`, we’ll add it to the component’s state.
```jsx
const [imageURL, setImageURL] = useState(null);
const [error, setError] = useState(null);
```

And finally, to assign `error` a value when a request fails, we’ll add a conditional to check the response status, and set it where our console.error line was.
```jsx
useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
    .then((response) => {
      if (response.status >= 400) {
        throw new Error("server error");
      }
      return response.json();
    })
    .then((response) => setImageURL(response[0].url))
    .catch((error) => setError(error));
}, []);
```
Notice how we also handle errors in the `then` block? This is because the `fetch` request itself might not fail, but rather complete successfully and yield a response. However, the response received may not be what our app expected. To handle this case, we check the response status codes.

Now when a bad URL is passed or the API returns an unexpected response, the page will relay that information to the user.
#### Loading state

In the same way we added an error value in state to check for errors, we can also add a loading value to check whether the request is resolved or not.
```jsx
const Image = () => {
  const [imageURL, setImageURL] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
      .then((response) => {
        if (response.status >= 400) {
          throw new Error("server error");
        }
        return response.json();
      })
      .then((response) => setImageURL(response[0].url))
      .catch((error) => setError(error))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>A network error was encountered</p>;

  return (
    <>
      <h1>An image</h1>
      <img src={imageURL} alt={"placeholder text"} />
    </>
  );
};
```
### Using custom hooks

We can separate out the fetching logic altogether into a custom hook. This will allow us to make the logic reusable and easily testable.

Recall in the [Introduction to state](https://www.theodinproject.com/lessons/node-path-react-new-introduction-to-state) lesson we said that a React hook is just a function that lets you use features of React (like states, effects etc.) and that they follow a naming rule where they begin with `use` followed by a capital letter (e.g. `useState` or `useEffect`). If we tried to put a hook such as `useEffect` inside our own regular helper function like `getImageURL`, React would not be happy about this since it only wants hooks to be called in the top level of a component or another hook. Therefore, we can just turn our helper function into a custom hook by following the hook naming rule - `useImageURL`.

Here’s how we would do it for our example:
```jsx
import { useState, useEffect } from "react";

const useImageURL = () => {
  const [imageURL, setImageURL] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/photos", { mode: "cors" })
      .then((response) => {
        if (response.status >= 400) {
          throw new Error("server error");
        }
        return response.json();
      })
      .then((response) => setImageURL(response[0].url))
      .catch((error) => setError(error))
      .finally(() => setLoading(false));
  }, []);

  return { imageURL, error, loading };
};

const Image = () => {
  const { imageURL, error, loading } = useImageURL();

  if (loading) return <p>Loading...</p>;
  if (error) return <p>A network error was encountered</p>;

  return (
    <>
      <h1>An image</h1>
      <img src={imageURL} alt={"placeholder text"} />
    </>
  );
};
```

If we ever needed to fetch images in different components, instead of rewriting all of that fetching logic we could call `useImageURL`.

### Managing multiple fetch requests

In a full-scale web app, you’re often going to be making more than one request, and you need to be careful with how you organize them. A common issue that new React developers face when their apps start making multiple requests is called a *waterfall of requests*. Let’s look at an example.

We have two components making fetch requests: `Profile` and its child component `Bio`. The requests in `Profile` and `Bio` are both firing inside of their respective components. On the surface this looks like a well-organized separation of concerns, but in this case, it comes at a cost in performance.

Notice how `Bio` is taking an extra second to display? Their fetch requests should both take 1000ms to resolve so what’s going on? In React, the component is not rendered until it is actually called. If JSX has conditional logic, the false branches will never render until they become true. `Bio` has to wait for the request inside of `Profile` to resolve before it starts rendering, which means the request inside `Bio` isn’t sent.

If we remove the short-circuiting conditional that waits for `imageURL`, `Bio` would send a request immediately, but that would mean abandoning our loading screen. Instead of compromising on design, we can lift the request up the component tree and pass its response as a prop to `Bio`.

To see this in action, go back to that embedded CodeSandbox and comment out the current `Profile` and `Bio` components, and uncomment the currently commented ones.

Now we have both requests firing as soon as `Profile` renders. The request for `imageURL` resolves 2 seconds before the `bioText` request, and our div containing `<Bio />` renders. When `bioText` resolves, an update will be made in state which will trigger a rerender in `<Bio />`, adding that text description to the page.

In all of the code examples above, we added an artificial `delay` with the `setTimeout` function. As you’ve likely guessed by now, this is to help you walk through the data fetching basics in the lesson. We recommend removing these `delay`s and play around with the code examples to further cement the concepts.
#### Promise.all to fire all at once
See https://www.developerway.com/posts/how-to-fetch-data-in-react#part5

### Data fetching libraries

We’ve only just begun to scratch the surface of data fetching on the frontend. Keeping your frontend data up-to-date with the server is a challenging task to accomplish. Managing “async” state becomes increasingly complex with each added feature.

You’ve already tasted the complexity of data fetching in this lesson. Each request has to have a *minimum* of three states to achieve an optimal user experience: `data`, `loading`, and `error`. Although some libraries can help you with data fetching and more, it is highly recommended to use vanilla React data fetching for all the projects in this course. The lessons you will learn while doing so will be invaluable.

