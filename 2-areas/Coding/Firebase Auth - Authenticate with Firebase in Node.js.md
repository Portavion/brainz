---
source: https://firebase.google.com/docs/auth/web/google-signin
author:
  - "[[Firebase]]"
created: 2025-02-07
Note Type:
  - Literary
category:
  - coding
status:
  - draft
---
# Authenticate with Firebase in Node.js
## Sign in the user
Sign in the user with their Google Account and get the user's Google ID token. For example:

If your app has a browser front end, use Google Sign-In as described in the [Handle the sign-in flow manually](https://firebase.google.com/docs/auth/web/google-signin#advanced-handle-the-sign-in-flow-manually) section. Get the Google ID token from the auth response:
```js
const id_token = googleUser.getAuthResponse().id_token
```
## Build a Credential object and sign-in the user with the credential
```js
import { getAuth, signInWithCredential, GoogleAuthProvider } from "firebase/auth";

// Build Firebase credential with the Google ID token.
const credential = GoogleAuthProvider.credential(id_token);

// Sign in with credential from the Google user.
const auth = getAuth();
signInWithCredential(auth, credential).catch((error) => {
  // Handle Errors here.
  const errorCode = error.code;
  const errorMessage = error.message;
  // The email of the user's account used.
  const email = error.customData.email;
  // The AuthCredential type that was used.
  const credential = GoogleAuthProvider.credentialFromError(error);
  // ...
});
```