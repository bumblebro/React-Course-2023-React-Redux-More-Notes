# Rendering the Root Component and Strict Mode

## Creating a React App from Scratch

### Importing React and ReactDOM

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
```

### Defining the App Component

```javascript
function App() {
  return <h1>Hello React!</h1>;
}
```

### Rendering the App Component to the DOM

```javascript
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

### Using Strict Mode

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### React v18 Rendering

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

### React v17 Rendering

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(<App />, document.getElementById('root'));
```
