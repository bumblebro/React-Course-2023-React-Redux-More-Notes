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
# What is JSX?

**Declarative Syntax and JSX in React**

**What is JSX?**

JSX is an extension to JavaScript that allows us to write HTML-like code in our JavaScript files. This makes it easier to describe the structure of our user interfaces, and it also allows us to embed JavaScript expressions directly into our HTML code.

**Why is JSX important in React?**

React is a JavaScript library for building user interfaces. It is declarative, which means that we describe what the UI should look like at all times, and React takes care of updating the DOM to match our description. JSX is a key part of React's declarative nature, as it allows us to describe our UI in a way that is both easy to read and write.

**How does JSX work?**

When we write JSX, it is actually converted to JavaScript code by a tool called Babel. This JavaScript code then tells React how to create the corresponding DOM nodes.

**What is the difference between imperative and declarative programming?**

Imperative programming is a style of programming where we write step-by-step instructions on how to achieve a particular result. Declarative programming, on the other hand, is a style of programming where we describe what we want to achieve, and the system (in this case, React) figures out how to achieve it.

**Why is declarative programming better for building UIs?**

Declarative programming is better for building UIs because it is easier to reason about and maintain. With declarative programming, we don't have to worry about the details of how the UI is updated, we only have to worry about what the UI should look like at all times. This makes our code easier to read and write, and it also makes it easier to debug.

**Here are some examples of code that uses JSX:**

```jsx
<div>
  <h1>Hello, world!</h1>
  <p>This is a paragraph.</p>
  <button onClick={() => console.log('Button clicked!')}>Click me</button>
</div>
```

This code will create a div element with an h1 element inside of it, a p element inside of it, and a button element inside of it. The button element will have an onClick handler that will log the message "Button clicked!" to the console when the button is clicked.

**Here is an example of how JSX is converted to JavaScript:**

```jsx
<div>
  <h1>Hello, world!</h1>
  <p>This is a paragraph.</p>
  <button onClick={() => console.log('Button clicked!')}>Click me</button>
</div>
```

This code is converted to the following JavaScript code:

```javascript
React.createElement('div', null, [
  React.createElement('h1', null, 'Hello, world!'),
  React.createElement('p', null, 'This is a paragraph.'),
  React.createElement('button', { onClick: () => console.log('Button clicked!') }, 'Click me'),
]);
```

As you can see, the JSX code is converted to a series of calls to the React.createElement function. This function is used to create React elements, which are the building blocks of React UIs.

**I hope this helps!**

# Creating More Components

Sure, here are the detailed notes with code from the paragraph given below:

**Header Component**

```javascript
function Header() {
  return (
    <header>
      <h1>Fast React Pizza Company</h1>
    </header>
  );
}
```

**Menu Component**

```javascript
function Menu() {
  return (
    <div className="menu">
      <h2>Our Menu</h2>
      <Pizza />
      <Pizza />
      <Pizza />
      <Pizza />
    </div>
  );
}
```

**Pizza Component**

```javascript
function Pizza() {
  return (
    <div className="pizza">
      <img src="pizza.jpg" alt="Pizza" />
      <h3>Margherita</h3>
      <p>A classic pizza with tomato sauce, mozzarella cheese, and basil.</p>
      <p>$12.99</p>
    </div>
  );
}
```

**Footer Component**

```javascript
function Footer() {
  return (
    <footer>
      <p>We're currently open. <br/> {new Date().toLocaleTimeString()}</p>
    </footer>
  );
}
```

**App Component**

```javascript
function App() {
  return (
    <div className="App">
      <Header />
      <Menu />
      <Footer />
    </div>
  );
}
```

**Code Snippets**

```javascript
// Display the current time
const date = new Date();
const timeString = date.toLocaleTimeString();
console.log(timeString);

// Combine JavaScript and JSX
const element = (
  <div>
    <h1>Hello, world!</h1>
    <p>The current time is {timeString}.</p>
  </div>
);

// Create a React element using createElement
const element = React.createElement('div', { className: 'App' }, [
  React.createElement('h1', null, 'Hello, world!'),
  React.createElement('p', null, 'The current time is {timeString}.'.format({ timeString })),
]);
```

**Key Points**

* JSX is a syntax extension to JavaScript that allows you to write HTML-like code directly in your JavaScript files.
* React components are reusable pieces of UI that can be nested together to create complex user interfaces.
* React uses a virtual DOM to efficiently update the UI in response to changes in state.

# JavaScript Logic in Components

Sure, here are detailed notes with code from the paragraph given below:

**Writing Logic Inside of React Components**

* Components are just JavaScript functions, so you can write any JavaScript in them that you want.
* Code is executed as soon as the function is caught, which is when the component is initialized.
* You can create new variables and use any JavaScript in the component.

**Example: Displaying an Alert in the App**

```javascript
const hour = new Date().getHours();
const openHour = 12;
const closeHour = 22;

let isOpen;
if (hour >= openHour && hour <= closeHour) {
  isOpen = true;
} else {
  isOpen = false;
}

console.log(isOpen);
```

**Notes:**

* The `alert()` function is used to display an alert in the app.
* The `isOpen` variable is used to store whether the restaurant is currently open or not.
* The `if/else` statement is used to determine whether the restaurant is open or not.

**Strict Mode**

* Components are usually rendered twice in strict mode.
* This is why the alert was displayed twice in the example above.

**Blocking JavaScript**

* The `alert()` function blocks JavaScript execution.
* This is why nothing else happened after the alert was displayed in the example above.

**Commented Code**

* The commented code is not currently being used, but it may be useful later.

**Variable Scope**

* The `isOpen` variable is declared outside of the `if/else` statement, so it is accessible throughout the component.
* This allows you to use the `isOpen` variable in other parts of the component.

I hope these notes are helpful!

# Separation of Concerns

Sure, here are detailed notes with code from the paragraph given below:

## React Components and Separation of Concerns

### Why React Components Combine HTML, CSS, and JavaScript

Prior to the rise of interactive single-page applications (SPAs), web development typically involved separate files for HTML, CSS, and JavaScript. This approach aligned with the traditional separation of concerns, where each technology handled a specific aspect of the user interface (UI).

However, with the increasing complexity of SPAs, JavaScript became more deeply involved in managing the UI, tightly coupling logic and presentation. This tight coupling led to the question of whether maintaining separate files for HTML, CSS, and JavaScript was still necessary.

React components emerged as a response to this question. They provide a way to encapsulate data, logic, and appearance for a specific UI element within a single unit. This approach aligns with the principle of co-location, which suggests that things that change together should be placed as close together as possible.

### JSX and Component Structure

JSX is a syntax extension to JavaScript that allows embedding HTML-like structures directly within JavaScript code. This enables developers to write components in a more declarative way, clearly defining the UI structure and its associated logic.

A typical React component might include:

- **Data:** The component's state or props, which represent the information it needs to display.
- **Logic:** JavaScript functions that handle events, update state, and perform calculations.
- **Appearance:** JSX code that defines the HTML structure and CSS styles for the component's UI.

This combination of data, logic, and appearance within a single component is what distinguishes React from traditional approaches that separate these concerns across different files.

### Separation of Concerns in React

While React components combine HTML, CSS, and JavaScript, they still maintain a separation of concerns within a component. Each component is responsible for a specific piece of the UI, encapsulating its data, logic, and appearance. This modular approach promotes code reusability and maintainability.

### Advantages of React Components

React components offer several advantages over traditional approaches:

- **Encapsulation:** Components encapsulate data, logic, and appearance, making them self-contained units.
- **Reusability:** Components can be reused across different parts of an application, reducing code duplication.
- **Maintainability:** Components are easier to manage and update as they contain all relevant information in one place.
- **Declarative Style:** JSX allows for a more declarative approach to UI development, focusing on the desired state rather than how to achieve it.

While some developers initially resisted the idea of combining HTML, CSS, and JavaScript within React components, this approach has proven to be effective and has been widely adopted in modern web development.

# Styling React Applications

Sure, here are some detailed notes with code from the paragraph given below:

**Notes:**

* React components can contain CSS styles.
* There are many different ways of applying CSS to React applications.
* React doesn't care about how you style your components.
* You can use inline styling, external CSS, SAS files, CSS modules, styled components, or Tailwind CSS to style your components.
* Inline styling is the most straightforward way to style components in JSX.
* To use inline styling, you need to enter JavaScript mode (curly braces) and then create an object with properties for each CSS property you want to set.
* You can also include an external CSS file to style your React applications.
* To include an external CSS file, you need to import it in your JSX file using the `import` syntax.
* To apply a class from an external CSS file to a JSX element, you need to add the class name to the JSX element using the `className` prop.
* Global styles are not scoped to each particular component.
* You can use styled components to create CSS that only belongs to one single component.

**Code:**

```jsx
import React from 'react';
import './index.css';

const App = () => {
  return (
    <div className="container">
      <header className="header">
        <h1>React Styling</h1>
      </header>

      <main className="menu">
        <ul>
          <li>Home</li>
          <li>About</li>
          <li>Contact</li>
        </ul>
      </main>

      <footer className="footer">
        <p>&copy; 2023 React Tutorial</p>
      </footer>
    </div>
  );
};

export default App;
```

```css
.container {
  background-color: #f0f0f0;
  font-family: sans-serif;
  padding: 20px;
}

.header {
  background-color: #007bff;
  color: #fff;
  padding: 20px;
}

.menu {
  background-color: #f5f5f5;
  padding: 20px;
}

.footer {
  background-color: #333;
  color: #fff;
  padding: 20px;
  text-align: center;
}
```

# Passing and Receiving Props
## Detailed Notes with Code

### Introducing Props

Props are a fundamental concept in React that allows you to pass data between components. They act as a communication channel between parent and child components.

### Customizing Pizza Components

1. **Passing Props from Parent to Child:**
   - Define props in the parent component using HTML attribute-like syntax.
   - Example:
     ```javascript
     <Pizza name="Pizza Spinaci" image="pizza-spinaci.jpg" ingredients="Tomato, Spinach, Mozzarella" price="10" />
     ```

2. **Receiving Props in Child Component:**
   - Accept a `props` parameter in the child component.
   - Example:
     ```javascript
     function Pizza(props) {
       return (
         <div className="pizza">
           <img src={props.photoName} alt={props.name} />
           <div>
             <h2>{props.name}</h2>
             <p>{props.ingredients}</p>
             <span>Price: {props.price}</span>
           </div>
         </div>
       );
     }
     ```

### Creating Multiple Pizza Components

1. **Create multiple pizza components, each with different props.**
   - Example:
     ```javascript
     <Pizza name="Pizza Funghi" image="pizza-funghi.jpg" ingredients="Tomato, Mushrooms, Mozzarella" price="12" />
     ```

2. **Customize CSS for pizza components.**
   - Use a CSS class `.pizza` to style the pizza components.
   - Example:
     ```css
     .pizza {
       display: flex;
       flex-direction: column;
       align-items: center;
       margin-bottom: 20px;
     }

     .pizza img {
       width: 200px;
       height: auto;
       margin-bottom: 10px;
     }

     .pizza h2 {
       font-size: 24px;
       margin-bottom: 5px;
     }

     .pizza p {
       font-size: 16px;
       margin-bottom: 10px;
     }

     .pizza span {
       font-size: 18px;
       font-weight: bold;
     }
     ```

### Dynamically Adding Numbers to Prices

1. **Pass prices as numbers instead of strings.**
   - Example:
     ```javascript
     <Pizza name="Pizza Spinaci" image="pizza-spinaci.jpg" ingredients="Tomato, Spinach, Mozzarella" price={10} />
     ```

2. **Use JavaScript mode to convert prices to numbers when necessary.**
   - Example:
     ```javascript
     <span>Price: {props.price + 3}</span>
     ```

### Flexibility of Props

- Props can be any data type, including objects, arrays, or even other React components.
- Props provide a powerful way to customize and reuse React components.

