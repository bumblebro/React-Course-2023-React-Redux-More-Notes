Sure, here are the detailed notes from the paragraph with coding examples:

**Project Setup**

* Delete all unnecessary files from the project folder.
* Create a new file named `index.js`.

**Importing React and ReactDOM**

* Import `React` from `react`.
* Import `ReactDOM` from `react-dom/client`.

**Creating the App Component**

* Create a function component named `App`.
* Return an `<h1>` element with the text "Hello React!".

**Rendering the App Component**

* Create a root element using `ReactDOM.createRoot()`.
* Select the `div` element with the id `"root"`.
* Render the `App` component to the root element.

**React v18 Rendering**

* Use the `root.render()` method to render the app.

**Strict Mode**

* Wrap the app component in a `React.StrictMode` component.
* Strict mode helps to find potential bugs and outdated React API usage.

**Coding Examples**

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';

const App = () => {
  return (
    <h1>Hello React!</h1>
  );
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import StrictMode from 'react/strict-mode';

const App = () => {
  return (
    <h1>Hello React!</h1>
  );
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
