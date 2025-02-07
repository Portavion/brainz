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
## Initial setup
Enable Google as a sign-in method in the Firebase console:
1. In the [Firebase console](https://console.firebase.google.com/), open the **Auth** section.
2. On the **Sign in method** tab, enable the **Google** sign-in method and click **Save**.
## Handle the sign-in flow with the Firebase SDK
### Create an instance of the Google provider object:
```js
import { GoogleAuthProvider } from "firebase/auth";

const provider = new GoogleAuthProvider();
```
### **Optional**: Specify additional OAuth 2.0 scopes that you want to request from the authentication provider
To add a scope call:
```js
provider.addScope('https://www.googleapis.com/auth/contacts.readonly');
```
### **Optional**: To localize the provider's OAuth flow to the user's preferred language
```js
import { getAuth } from "firebase/auth";

const auth = getAuth();
auth.languageCode = 'it';
// To apply the default browser preference instead of explicitly setting it.
// auth.useDeviceLanguage();
```
### **Optional**: Specify additional custom OAuth provider parameters that you want to send with the OAuth request
```js
provider.setCustomParameters({
  'login_hint': 'user@example.com'
});
```
### Authenticate with Firebase using the Google provider object
To sign in with a pop-up window, call **signInWithPopup**:
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
To sign in by redirecting to the sign-in page, call **signInWithRedirect**: Follow the [best practices](https://firebase.google.com/docs/auth/web/redirect-best-practices) when using `signInWithRedirect`.
```js

```