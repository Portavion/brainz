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
# Firebase Auth - Google Signup
## Initial Setup
Enable Google as a sign-in method in the Firebase console:
1. In the [Firebase console](https://console.firebase.google.com/), open the **Auth** section.
2. On the **Sign in method** tab, enable the **Google** sign-in method and click **Save**.
## Handle the Sign-in Flow with the Firebase SDK
### Create an Instance of the Google Provider Object:
```js
import { GoogleAuthProvider } from "firebase/auth";

const provider = new GoogleAuthProvider();
```
### **Optional**: Specify Additional OAuth 2.0 Scopes that You want to Request from the Authentication Provider
To add a scope call:
```js
provider.addScope('https://www.googleapis.com/auth/contacts.readonly');
```
### **Optional**: To Localize the Provider's OAuth Flow to the User's Preferred Language
```js
import { getAuth } from "firebase/auth";

const auth = getAuth();
auth.languageCode = 'it';
// To apply the default browser preference instead of explicitly setting it.
// auth.useDeviceLanguage();
```
### **Optional**: Specify Additional Custom OAuth Provider Parameters that You want to Send with the OAuth Request
```js
provider.setCustomParameters({
  'login_hint': 'user@example.com'
});
```
### Authenticate with Firebase Using the Google Provider Object
To sign in with a pop-up window, call **`signInWithPopup`**:
```js
import { getAuth, signInWithPopup, GoogleAuthProvider } from "firebase/auth";

const auth = getAuth();
signInWithPopup(auth, provider)
  .then((result) => {
    // This gives you a Google Access Token. You can use it to access the Google API.
    const credential = GoogleAuthProvider.credentialFromResult(result);
    const token = credential.accessToken;
    // The signed-in user info.
    const user = result.user;
    // IdP data available using getAdditionalUserInfo(result)
    // ...
  }).catch((error) => {
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
To sign in by redirecting to the sign-in page, call `signInWithRedirect`: Follow the [best practices](https://firebase.google.com/docs/auth/web/redirect-best-practices) when using `signInWithRedirect`.
```js
import { getAuth, signInWithRedirect } from "firebase/auth";

const auth = getAuth();
signInWithRedirect(auth, provider);
```
Then, you can also retrieve the Google provider's OAuth token by calling `getRedirectResult` when your page loads:
```js
import { getAuth, getRedirectResult, GoogleAuthProvider } from "firebase/auth";

const auth = getAuth();
getRedirectResult(auth)
  .then((result) => {
    // This gives you a Google Access Token. You can use it to access Google APIs.
    const credential = GoogleAuthProvider.credentialFromResult(result);
    const token = credential.accessToken;

    // The signed-in user info.
    const user = result.user;
    // IdP data available using getAdditionalUserInfo(result)
    // ...
  }).catch((error) => {
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