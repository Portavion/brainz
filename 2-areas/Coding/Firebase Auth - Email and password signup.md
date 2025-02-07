---
source: 
author: 
created: 2025-02-07
Note Type:
  - Literary
category:
  - coding
status:
  - draft
---
# Getting Started with Firebase Auth
## Initialise Firebase Auth
Initialise the Firebase Auth inside firebase.config.js
```js
import { getAuth } from "firebase/auth";

// Initialize Firebase Authentication and get a reference to the service
const auth = getAuth(app);
```
## Signup New Users
Create a form that allows users to signup with email and password. When submitted, validate the inputs and pass them to the **createUserWithEmailAndPassword** method:
```js
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";

const auth = getAuth();
createUserWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed up 
    const user = userCredential.user;
    // ...
  })
  .catch((error) => {
    const errorCode = error.code;
    const errorMessage = error.message;
    // ..
  });
```

## Signup Existing Users
Create a form that allows existing users to sign in using their email address and password. When a user completes the form, call the **signInWithEmailAndPassword** method:
```js
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";

const auth = getAuth();
signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in 
    const user = userCredential.user;
    // ...
  })
  .catch((error) => {
    const errorCode = error.code;
    const errorMessage = error.message;
  });
```
## Setup the Auth State Observer and Get User Data
For each of your app's pages that need information about the signed-in user, attach an observer to the global authentication object. This observer gets called whenever the user's sign-in state changes.

Attach the observer using the **onAuthStateChanged** method. When a user successfully signs in, you can get information about the user in the observer.
```js
import { getAuth, onAuthStateChanged } from "firebase/auth";

const auth = getAuth();
onAuthStateChanged(auth, (user) => {
  if (user) {
    // User is signed in, see docs for a list of available properties
    // https://firebase.google.com/docs/reference/js/auth.user
    const uid = user.uid;
    // ...
  } else {
    // User is signed out
    // ...
  }
});
```