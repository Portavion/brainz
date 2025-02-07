---
title: "A future-proof Node.js express file/folder structure"
source: "https://www.codemzy.com/blog/nodejs-file-folder-structure"
author:
  - "[[Codemzy]]"
published: 2022-11-28
created: 2025-01-15
description: "How should we structure folders and files in Node.js? I was unhappy and slightly confused by the MVC approach, and wanted to move to a more colocation/feature-based structure. Here's what I came up with."
tags:
  - "clippings"
---
# A Future-proof Node.js Express Filefolder Structure
How should we structure folders and files in Node.js? I was unhappy and slightly confused by the MVC approach, and wanted to move to a more colocation/feature-based structure. Here's what I came up with.

This blog post is heavily influenced by a fantastic tutorial by Joshua Comeau about [ReactJS file/directory structures](https://www.joshwcomeau.com/react/file-structure/). It's well worth a read if you use React.

After whipping my front-end code from chaos to cleanly organised (thanks Josh!), I decided to tackle the server-side code.

## Node.js + Express

For the server, I'm using Node.js and Express. Express is described as a *"fast, unopinionated, minimalist web framework for Node.js"*.

Which is great. **Unopinionated** means you can structure your files however you want. But it's also bad. Because you can structure your files however you want!

But after much internal debating, and some sleepless nights (seriously!) - I've come up with a new Node.js folder structure that I'm finally\* happy with!

\**Nothing is ever really permanent, but I'll keep this post updated if anything changes!*

So, before we get into the details, let's take a look at an example. Here's how I'd structure an API for a library, which will have books and allow users to borrow them.

```
📁 server/
└── 📁 api/
  └── 📁 books/
    ├── 📄 books.js
    ├── 📄 books.handlers.js
    ├── 📄 books.routes.js
    └── 📄 index.js
  ├── 📁 borrow/
    ├── 📄 borrow.js
    ├── 📄 borrow.handlers.js
    ├── 📄 borrow.helpers.js
    ├── 📄 borrow.routes.js
    └── 📄 index.js
  ├── 📁 user/
    ├── 📄 index.js
    ├── 📄 user.js
    ├── 📄 user.handlers.js
    ├── 📄 user.helpers.js
    ├── 📄 user.middleware.js
    └── 📄 user.routes.js
├── 📁 middleware/
├── 📁 utils/
├── 📄 routes.js
└── 📄 server.js
```

I'll dive more into the details of this structure shortly, but first, why have I ditched the other common approach, MVC?

## What about MVC?!

If you look at most Node.js tutorials, and certainly when I was learning Node.js, you're going to see the MVC (Model, View, Controller) structure.

But in my experience, it usually ends up being more MVCSRM (Model, View, Controller, Services, Routes, Middleware) with a directory for each.

Here's an example of a folder structure in Node.js with MVC\*:

\**I've left out `views` because this is an API, but you could add that extra directory if you are serving HTML from the server.*

```
📁 server/
├── 📁 controllers/
  ├── 📄 books.controllers.js
  ├── 📄 borrow.controllers.js
  └── 📄 user.controllers.js
├── 📁 routes/
  ├── 📄 books.routes.js
  ├── 📄 borrow.routes.js
  ├── 📄 index.js
  └── 📄 user.routes.js
├── 📁 services/
  ├── 📄 books.services.js
  ├── 📄 borrow.services.js
  └── 📄 user.services.js
├── 📁 helpers/
  ├── 📄 borrow.helpers.js
  └── 📄 user.helpers.js
├── 📁 middleware/
  └── 📄 user.middleware.js
├── 📁 utils/
└── 📄 server.js
```

I don't hate this pattern. I've used it on a few projects and it gets the job done. But as new features get added/updated/removed it becomes harder to keep track of all the files.

When the directories are closed, every project looks the same.

```
📁 server/
├── 📁 controllers/
├── 📁 routes/
├── 📁 services/
├── 📁 helpers/
├── 📁 middleware/
├── 📁 utils/
└── 📄 server.js
```

At first glance, I really don't know what this server does. And I need to open up every directory to find out which ones each feature uses.

For example, let's say I need to add a new endpoint to books. I've got to open the `routes`, `controllers`, `services` and probably `helpers` too. Then open up all the files relating to `books`.

You've got to open all those different directories to check which files relate to books. For example, there's no `books.helpers.js` file, but you wouldn't know until you check the `helpers` directory.

And what if you want to add other files for validation, constants, or other functions? Do you add a `validation`, and `constants` directory? Or maybe a global `validation.js` and `constants.js` in each directory?

Whenever I hit these questions, everything started to feel a little over-engineered.

I also read [Kent C. Dodds post about colocation](https://kentcdodds.com/blog/colocation) and felt like I should try to make my code more colocated on the server.

With my new folder structure, I can head straight to the `books` directory, and all the files I need are in one place.

```
📁 server/
└── 📁 api/
  └── 📁 books/
    ├── 📄 books.js
    ├── 📄 books.handlers.js
    ├── 📄 books.routes.js
    └── 📄 index.js
```

You instantly know which files relate to books because they are all neatly together in one place.

It's also more future-proof for the inevitable changes (and [versions](https://www.codemzy.com/blog/nodejs-api-versioning)) that will happen throughout the life of your code.

If I want to add a separate file for validation, I just add a `books.validation.js` file to the `books` directory. If I want to add some helper functions, I can add `books.helpers.js`. Any files I need for books, go into the `books` directory. Simple.

And let's say our library decided to get rid of books, and loan games instead. I can just delete the `books` directory, instead of fumbling about opening every other folder looking for files with `books` in the title.

Or if you want to upgrade your server to a totally different framework or code library, you can do it incrementally, one directory at a time. Upgrade `books` now and `borrowing` later.

If you need to move your files or rename `books` to `booksV1`\*, you'll only need to change one import statement.

\**For adding versioning, I came up with some options in [Future-proof API versioning with Node.js & Express](https://www.codemzy.com/blog/nodejs-api-versioning).*

I'm not saying my approach is *best practice*, or better than MVC - but it works better for me. If you are struggling with the MVC approach, maybe this type of colocation will work better for you too.

## The Structure

Ok, let's take a more detailed look at this alternative folder structure for Node.js and see how it works.

### API

I call this first folder `api` but if your server is more than an API, and serves HTML too, you could call it `app` or `features`.

And while you might feel that this folder is organised by *features*, I prefer to think of it as organised by *path* or *route*.

Let's say the API has the following routes:

```js
// get a list of books
api.mylibrary.com/books GET
// add a new book
api.mylibrary.com/books POST
// get a book
api.mylibrary.com/books/:id GET
// update a book
api.mylibrary.com/books/:id POST

// list of borrowed books
api.mylibrary.com/borrow GET
// borrow a book
api.mylibrary.com/borrow POST

// get user info
api.mylibrary.com/users GET
// get a user
api.mylibrary.com/users/:id GET
// update a user
api.mylibrary.com/users/:id POST
```

You can see that the URL structure shows the different services, `books`, `borrow` and `user`. And I want my Node.js folder structure to reflect that.

```
📁 server/
└── 📁 api/
  ├── 📁 books/
  ├── 📁 borrow/
  ├── 📁 user/
├── 📁 helpers/
├── 📁 middleware/
├── 📁 utils/
├── 📄 routes.js
└── 📄 server.js
```

And here's an example of what's included in the `books` folder.

```
📁 server/
└── 📁 api/
  └── 📁 books/
    ├── 📄 books.js
    ├── 📄 books.handlers.js
    ├── 📄 books.routes.js
    └── 📄 index.js
```

You can name the files inside books whatever you like. The thing to remember is that any file that only relates to books, belongs in the `books` directory.

When I need to add a new base route, like `api.mylibrary.com/games`, I'll add a `games` folder to the `api` directory.

The great thing about this pattern is everything for games will be in that new directory. If I need to add a new route for games, I can open up the folder and everything I need is in one place. The games specific routes, middleware and helpers are all used together and stored together.

### Routes

I set up my main route structure in `routes.js`. This file ties all of the different features of the server together.

```
📁 server/
└── 📁 api/
  ├── 📁 books/
  ├── 📁 borrow/
  ├── 📁 user/
├── 📁 helpers/
├── 📁 middleware/
├── 📁 utils/
├── 📄 routes.js <---
└── 📄 server.js
```

For example, `routes.js` will say any routes starting with `/books` will be handled by the `./api/books` directory.

```js
// import the routes for '/books'
const bookRoutes = require('./api/books');
// or ES6 module
// import bookRoutes from './api/books';

// wire up to the express app
app.use('/api/books', bookRoutes);
```

You can either use the full file name `./api/books/books.routes.js` or simplify the import (like I've done above) by exporting it from `books/index.js`.

Here's how `/api/books/index.js` would look in common js.

```js
// export the book router
module.exports = require('./books.routes');
```

And here's how it looks in ES6.

```js
export { default } from './books.routes';
```

I like doing this and it's one of the benefits of this Node.js folder structure - the `routes.js` file is the only file you need outside of the directory, so it's the only thing you need to export!

Now we handle the routes for `/api/books` in - you guessed it - the `books` directory.

```
📁 server/
└── 📁 api/
  └── 📁 books/
    ├── 📄 books.js
    ├── 📄 books.handlers.js
    ├── 📄 books.routes.js <---
    └── 📄 index.js
```

Here's how that might look:

```js
const express = require('express');
const booksRoutes = express.Router();
// or ES6
// import { Router as booksRoutes } from 'express';

// Handlers
const booksHandlers = require('./books.handlers');

// list all books
booksRoutes.get('/', booksHandlers.books);

// export bookRoutes 
module.exports = booksRoutes;
// or ES6
// export default booksRoutes;
```

### Handlers

You've probably noticed the `.handlers.js` files and wondered what they are about.

You could also call these functions `controllers`, but I chose `handlers` because it’s shorter and I felt it was clearer since I wasn’t strictly following the `MVC` approach.

> HANDLER is the function executed when the route is matched.
> 
> — ExpressJS - [Basic routing](https://expressjs.com/en/starter/basic-routing.html)

Routes call the handlers, and the handler handles the request. It's responsible for taking a request and calling any functions it needs to send a response.

Here's an example from `books.handlers.js`.

```js
const { listBooks } = require('./books');

exports.books = async function(req, res) {
  const { user } = req.body
  const filters = req.query;
  try {
    // get list of books
    const result = await listBooks({ user, filters });
    res.json(result);
  } catch(e) {
    console.log(e.message)
    res.status(500).send({ error: 'Problem fetching books.' });
  }
}
```

### Features

The handler will call functions that contain the business logic, for example, a `listBooks` function that reaches out to the database to fetch a list of books.

In the MVC pattern, these are called services or workers.

I tend to put these functions in the main `books.js` file, but the nice thing about this pattern is you can call them whatever you like. You could have each function in a different file, `getBooks.js` and `getBook.js` - or keep these functions together in one file.

### Helpers/Utils

Any function used by `books` that are not used anywhere else can stay in the `books` directory. I call these `helpers` e.g. `books.helpers.js` because they are specific to help that feature or service.

If it's more of a generic function used throughout the services, then I put those functions in the `server/utils` folder.

### Middleware

The same as `utils`. If the middleware is specific to a feature, I'll put it in that features directory, e.g. `books.middleware.js`. But if it's shared with other parts of the server, I'll put it in the `server/middleware` folder.

Another benefit to this approach is I know what files and functions are only used in one place, and which ones are shared - which is useful when removing routes or features.

### Views

In this API example, I haven't included views. I actually wouldn't have a `books.views.[ext]` file, but you could do that if it makes sense. If I was generating views on the backend (rather than building an API), I'd still want to keep them separate from the data.

I'd create a `html` or `components` folder and [structure the files like this](https://www.joshwcomeau.com/react/file-structure/).

```
📁 server/
└── 📁 api/
  ├── 📁 books/
  ├── 📁 borrow/
  ├── 📁 user/
├── 📁 helpers/
├── 📁 html/ <---
├── 📁 middleware/
├── 📁 utils/
├── 📄 routes.js
└── 📄 server.js
```

### The Kitchen Sink

You can expand this as much as you like. For example, `books.models.js`, `books.constants.js`, or `books.validation.js`.

You could even break this down even further and have one directory for each end route. It might sound crazy but I strongly considered it.

However, I found that often you'll share a lot of validation and helpers between each route for a specific service, e.g. all routes starting with `books`, so I didn't take it that far!

---

I really like this approach. I've found it much simpler to work on the server-side code since refactoring with this approach. Now when I'm working on a specific feature, I only have to open up one directory and all the code I need is there.

And as a side effect, your imports become much simpler - now that most of your imported code lives in the same directory.

**What about API versions? Check out my post on [API versioning with Node.js](https://www.codemzy.com/blog/nodejs-api-versioning) for how I came up with my future-proof way to add versioning to this file structure.**