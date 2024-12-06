# Project creation with Vite
## Template
Run:
```bash
npm create vite@latest my-first-react-app -- --template react
```
Then follow the instructions or:
```bash
cd my-first-react-app
npm install
npm run dev

```
## Testing suite
### Vitest
Install the testing suite
```bash
npm install vitest --save-dev
```
Then in your package.json file, add another script which will run the tests eventually:
```json
{
  ...
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "test": "vitest",
    "preview": "vite preview"
  },
  ...
}
```

Create a test file somewhere in your project with the suffix _test_, e.g. _App.test.jsx_, and give it the following content:
```javascript
import { describe, it, expect } from 'vitest';
describe('something truthy and falsy', () => {
  it('true to be true', () => {
    expect(true).toBe(true);
  });
  it('false to be false', () => {
    expect(false).toBe(false);
  });
});
```
### jsdom
```bash
npm install jsdom --save-dev
```
then in the Vite configuration file:
```json
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    environment: 'jsdom',
  },
});
```
Then install the react testing library:
```bash
npm install @testing-library/react @testing-library/jest-dom --save-dev
```
Fourth, add a test setup file in _tests/setup.js_ and give it the following implementation:
```javascript
import { expect, afterEach } from 'vitest';
import { cleanup } from '@testing-library/react';
import * as matchers from "@testing-library/jest-dom/matchers";
expect.extend(matchers);
afterEach(() => {
  cleanup();
});
```
And last, include this new test setup file in Vite's configuration file. In addition, make all imports from Vitest global, so that you don't need to perform these imports (e.g. `expect`) in each file manually anymore:
```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './tests/setup.js',
  },
});
```
That's it. You can render React components in Vitest now:
```javascript
import { render, screen } from '@testing-library/react';
import App from './App';
describe('App', () => {
  it('renders headline', () => {
    render(<App title="React" />);
    screen.debug();
    // check if App components renders headline
  });
});
```
Last final package:
```bash
npm install @testing-library/user-event --save-dev
```
## GitHub
To link your local project directory to a GitHub repo, create a new **empty** repo on GitHub then follow the instructions in the new repo’s page to connect it to your local project directory.

Alternatively, if you created a GitHub repo already and cloned it, you can `cd` into your cloned repo then run the above Vite command, using `.` as the project name:
```bash
npm create vite@latest . -- --template react
```
This will tell Vite to use the current directory for the project, instead of creating a new directory with the given project name. This cloned directory will already be initialized as a git repo and connected to the right remote.