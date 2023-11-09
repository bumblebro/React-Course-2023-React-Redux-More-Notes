
## Pure React

### Introduction

This section provides an overview of pure React and demonstrates how to write React code without any modern tooling or build step.

### Setting up the project

1. Create a project folder named "01-pure-React".
2. Open the project folder in VS Code.
3. Create an empty HTML file named "index.HTML".
4. Add a title to the HTML file: `"Hello React!"`.
5. Create a div element with the ID "root" in the body of the HTML file: `<div id="root"></div>`.

### Adding React libraries

1. Include the React and React-dom libraries in the HTML file:

```html
<script src="https://unpkg.com/react@17/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```

### Creating the first React component

1. Create a JavaScript function named "App":

```javascript
function App() {
  return React.createElement('header', null, 'Hello React!');
}
```

### Rendering the component

1. Render the App component into the root div:

```javascript
const root = React.createRoot(document.getElementById('root'));
root.render(React.createElement(App));
```

### Updating the component with state

1. Create a state variable named "time":

```javascript
const [time, setTime] = React.useState(new Date().toLocaleTimeString());
```

2. Update the time state every second using setInterval:

```javascript
React.useEffect(() => {
  const intervalId = setInterval(() => {
    setTime(new Date().toLocaleTimeString());
  }, 1000);
  return () => clearInterval(intervalId);
}, []);
```

3. Display the current time in the header:

```javascript
return React.createElement('header', null, `Hello React! It's ${time}`);
```

### Conclusion

This example demonstrates how to write pure React code without any modern tooling or build step. However, it is important to note that this approach is not recommended for production use due to its lack of features and tooling support.
