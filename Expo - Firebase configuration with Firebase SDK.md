---
source: https://docs.expo.dev/guides/using-firebase/
author: "[[Expo]]"
created: 2025-02-07
Note Type:
  - Literary
category:
  - coding
status:
  - draft
---
# Expo - Firebase configuration with Firebase SDK
Create a new project in the Firebase console.
## Install the Firebase SDK:
```shell
npx expo install firebase
```
## Initialise the SDK in the project:
 ```js
 // firebaseConfig.js
 import { initializeApp } from 'firebase/app';

// Optionally import the services that you want to use
// import {...} from 'firebase/auth';
// import {...} from 'firebase/database';
// import {...} from 'firebase/firestore';
// import {...} from 'firebase/functions';
// import {...} from 'firebase/storage';

// Initialize Firebase
const firebaseConfig = {
  apiKey: 'api-key',
  authDomain: 'project-id.firebaseapp.com',
  databaseURL: 'https://project-id.firebaseio.com',
  projectId: 'project-id',
  storageBucket: 'project-id.appspot.com',
  messagingSenderId: 'sender-id',
  appId: 'app-id',
  measurementId: 'G-measurement-id',
};

const app = initializeApp(firebaseConfig);
// For more information on how to access Firebase in your project,
// see the Firebase documentation: https://firebase.google.com/docs/web/setup#access-firebase
```
## Configure Metro
If metro.config.js doesn't already exists in your config then generate it with:
```shell
npx expo customize metro.config.js
```

Then update the file with the following configuration:
```js
// metro.config.js
const { getDefaultConfig } = require('@expo/metro-config');

const defaultConfig = getDefaultConfig(__dirname);
defaultConfig.resolver.sourceExts.push('cjs');

module.exports = defaultConfig;

```
## Next steps
[[Getting started with Firebase Auth]]
