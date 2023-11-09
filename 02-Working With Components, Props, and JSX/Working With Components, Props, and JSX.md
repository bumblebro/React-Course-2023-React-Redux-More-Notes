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

# Components as Building Blocks

Sure, here are detailed notes with code from the paragraph given below:

**Components in React**

Components are the fundamental building blocks of React applications. They are self-contained units of code that encapsulate data, logic, and appearance. Each component can be thought of as a piece of the user interface (UI).

**Key Concepts**

* **Component:** A piece of the UI that has its own data, JavaScript logic, and appearance.
* **Component Tree:** A hierarchical representation of the components that make up a React application.
* **Parent Component:** A component that contains other components.
* **Child Component:** A component that is contained within another component.
* **Nesting:** The process of placing components inside of other components.
* **Props:** A way to pass data from a parent component to a child component.

**Code Example**

```javascript
function Question(props) {
  return (
    <div className="question">
      <h2>{props.title}</h2>
      <p>{props.body}</p>
    </div>
  );
}

function VideoPlayer() {
  return (
    <div className="video-player">
      <video src="..." controls></video>
    </div>
  );
}

function Menu() {
  return (
    <ul className="menu">
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  );
}

function RefinedQuestions() {
  return (
    <div className="refined-questions">
      <Filters />
      <Question title="What is the capital of France?" body="Paris" />
      <Question title="What is the largest country in the world?" body="Russia" />
      <Question title="What is the highest mountain in the world?" body="Mount Everest" />
    </div>
  );
}

function App() {
  return (
    <div className="app">
      <VideoPlayer />
      <Menu />
      <RefinedQuestions />
    </div>
  );
}
```

**Summary**

Components are essential for building complex and reusable user interfaces in React. By understanding the concepts of components, component trees, parent components, child components, nesting, and props, you can effectively create React applications that are easy to manage and maintain.

# Creating And Reusing a Component
Sure, here are the detailed notes with code from the paragraph given below:

**Creating a new component**

```jsx
function Pizza() {
  return (
    <div>
      <h2>Pizza</h2>
      <p>Spinach</p>
      <img src="/public/spinaci.jpg" alt="Spinach pizza" />
    </div>
  );
}
```

**Including the component**

```jsx
import Pizza from './Pizza';

function App() {
  return (
    <div>
      <Pizza />
      <Pizza />
      <Pizza />
    </div>
  );
}
```

**Using starter data**

```jsx
import Pizza from './Pizza';
import data from './data';

function App() {
  return (
    <div>
      {data.pizzas.map((pizza) => (
        <Pizza
          key={pizza.id}
          name={pizza.name}
          ingredients={pizza.ingredients}
        />
      ))}
    </div>
  );
}
```

**Reusing the component**

```jsx
import Pizza from './Pizza';
import data from './data';

function App() {
  return (
    <div>
      {data.pizzas.map((pizza) => (
        <Pizza
          key={pizza.id}
          name={pizza.name}
          ingredients={pizza.ingredients}
        />
      ))}
    </div>
  );
}
```

**Removing colored lines from the gutter**

1. Go to Settings.
2. Search for "diff decorations".
3. Set the default to "none".
