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

# Props, Immutability, and One-Way Data Flow## Detailed Notes with Code

### Props Review and Important Concepts

- Props are used to pass data from parent components to child components.
- Props are essentially settings that control the appearance and behavior of child components.
- Props can be any type of value, including single values, arrays, objects, functions, and even other React components.

### Props vs. State

- Props are external data owned by the parent component and cannot be modified by the child component.
- State is internal component data that can be updated by the component's logic.
- React enforces one-way data flow, meaning data can only flow from parent to child components, never the other way around.

### Reasons for One-Way Data Flow

- Predictability: One-way data flow makes it easier to understand where data comes from and how it affects the component tree.
- Debugging: One-way data flow simplifies debugging by reducing potential data conflicts and making it easier to track data changes.
- Performance: Two-way data binding can be less efficient and more difficult to optimize.

### State Management

- While props are read-only and immutable, state is dynamic and can be updated within the component.
- In the next section, we will learn how to manage state using React's state management techniques.


# The Rules of JSX
## Detailed Notes with Code

### General JSX Rules

- JSX syntax is similar to HTML, but you can enter JavaScript mode using curly braces.
- Inside JavaScript mode, you can place any JavaScript expression, including variables, arrays, objects, operators, but not statements.
- JSX produces a JavaScript expression, allowing you to nest JSX expressions and use JSX anywhere in a component.

### Implications of JSX as an Expression

1. Nested JSX Expressions: You can place JSX expressions inside curly braces, allowing you to embed expressions within expressions.

2. Flexibility of JSX Placement: You can write JSX anywhere inside a component, including assignments, if/else statements, functions, and more.

### Single Root Element Rule

- A piece of JSX can only have one root element, which acts as the parent element.
- To return multiple elements, use React Fragments (covered later).

### JSX vs. HTML Differences

- JSX allows JavaScript expressions within curly braces, while HTML doesn't.
- JSX uses camelCase for certain attributes, like `className` instead of `class`.
- JSX requires closing tags for self-closing elements, like `<hr/>`.

### Learning JSX Rules through Practice

- The best way to understand JSX rules is to write code and experiment with different scenarios.
- As you encounter these rules throughout the course, you'll gain a deeper understanding of JSX syntax and its flexibility.

  # Rendering Lists
  ## Detailed Notes with Code

### Rendering Lists with React's `map` Method

1. **Goal:** Render a unique component for each item in an array.

2. **Process:**
   a. Use the `map` method on the array to create a new array of components.
   b. Pass each item in the original array as a prop to the corresponding component in the new array.

### Example: Rendering Pizza Components

```jsx
const pizzas = [
  { name: "Pizza Spinaci", photoName: "pizza-spinaci.jpg", ingredients: "Tomato, Spinach, Mozzarella", price: 10 },
  { name: "Pizza Funghi", photoName: "pizza-funghi.jpg", ingredients: "Tomato, Mushrooms, Mozzarella", price: 12 },
  { name: "Pizza Margherita", photoName: "pizza-margherita.jpg", ingredients: "Tomato, Mozzarella", price: 9 },
];

const Pizza = (props) => (
  <div className="pizza">
    <img src={props.photoName} alt={props.name} />
    <div>
      <h2>{props.name}</h2>
      <p>{props.ingredients}</p>
      <span>Price: {props.price}</span>
    </div>
  </div>
);

const PizzaList = () => (
  <ul className="pizzas">
    {pizzas.map((pizza) => (
      <li key={pizza.name}>
        <Pizza {...pizza} />
      </li>
    ))}
  </ul>
);

<PizzaList />
```

### Avoiding `for` Loops in JSX

- JSX requires a consistent return value, which is not possible with `for` loops.
- Use `map` to create a new array of JSX elements, which React can render.


# Conditional Rendering With &&

**Conditional Rendering in React**

**Using the & Operator for Conditional Rendering**

The & operator can be used for conditional rendering in React. This works because of short-circuiting. Short-circuiting means that if the first operand of the & operator is falsey, then the second operand is not evaluated and the result of the operation is the first operand. This can be useful for conditionally rendering JSX based on a condition.

**Example:**

```jsx
const isOpen = currentHour >= 12 && currentHour <= 22;

if (isOpen) {
  return <p>Open</p>;
} else {
  return <p>Closed</p>;
}
```

**Using the Ternary Operator for Conditional Rendering**

The ternary operator can also be used for conditional rendering in React. The ternary operator takes three operands: a condition, a value to return if the condition is true, and a value to return if the condition is false.

**Example:**

```jsx
const isOpen = currentHour >= 12 && currentHour <= 22;

return <p>{isOpen ? "Open" : "Closed"}</p>;
```

**Which Operator to Use?**

Both the & operator and the ternary operator can be used for conditional rendering in React. The choice of which operator to use is a matter of preference. Some people prefer the & operator because it is more concise. Others prefer the ternary operator because it is more explicit.

**Additional Notes**

* **Do not use a number as the condition for conditional rendering.** This can lead to unexpected behavior because of short-circuiting.
* Always use a true or false condition for conditional rendering.

**Example Code**

```jsx
const pizzaData = [
  { name: "Margherita", price: 10 },
  { name: "Pepperoni", price: 11 },
  { name: "Hawaiian", price: 12 },
];

const isOpen = currentHour >= 12 && currentHour <= 22;

return (
  <div>
    <h2>Restaurant</h2>
    {isOpen && <p>Open until {closingHour}</p>}
    <p>Come visit us or order online!</p>
    <button className="btn order">Order Now</button>

    <ul>
      {pizzas.length > 0 && (
        <li>
          <h2>Pizzas</h2>
          {pizzas.map((pizza) => (
            <li key={pizza.name}>
              <h3>{pizza.name}</h3>
              <p>Price: ${pizza.price}</p>
            </li>
          ))}
        </li>
      )}
    </ul>
  </div>
);
```

# Conditional Rendering With Ternaries

**Conditional Rendering with the Ternary Operator**

The ternary operator can be used for conditional rendering in React. It has three operands: a condition, a value to return if the condition is true, and a value to return if the condition is false.

**Example:**

```jsx
const pizzas = pizzaData.length > 0 ? (
  <li>
    <h2>Pizzas</h2>
    {pizzas.map((pizza) => (
      <li key={pizza.name}>
        <h3>{pizza.name}</h3>
        <p>Price: ${pizza.price}</p>
      </li>
    ))}
  </li>
) : (
  <p>We're still working on our menu. Please come back later.</p>
);
```

**Advantages of Using the Ternary Operator**

* **More explicit:** The ternary operator makes it more explicit what the condition is and what the values are for the true and false cases.
* **Can display an alternative:** When the condition is false, the ternary operator can be used to display an alternative value instead of nothing.

**Why an If-Else Statement Cannot Be Used**

An if-else statement cannot be used for conditional rendering in React because it does not produce a value. JSX requires a value to be returned, and an if-else statement does not return a value.

**Overall**

The ternary operator is a powerful tool for conditional rendering in React. It is easy to use and can be used to display different JSX based on a condition.

# Conditional Rendering With Multiple Returns

**Conditional Rendering with Multiple Returns**

Conditional rendering with multiple returns is a technique that can be used to conditionally render different parts of a component. This is done by using multiple return statements inside the component, with each return statement returning a different block of JSX based on a condition.

**Example:**

```jsx
function Pizza(props) {
  if (props.pizza.soldOut) {
    return null;
  }

  return (
    <li>
      <h3>{props.pizza.name}</h3>
      <p>Price: ${props.pizza.price}</p>
    </li>
  );
}
```

**Advantages of Using Multiple Returns**

* **Flexibility:** Multiple returns allow for more flexibility in conditional rendering, as you can return different blocks of JSX or even different components based on a condition.
* **Clarity:** Using multiple returns can make your code more clear and readable, as it explicitly shows which parts of the component are being rendered under which conditions.

**When to Use Multiple Returns**

Multiple returns are typically used for conditionally rendering entire components, rather than just pieces of JSX. However, they can also be used for conditionally rendering JSX, especially when the conditional logic is more complex.

**Overall**

Conditional rendering with multiple returns is a powerful technique that can be used to create more dynamic and flexible React components. However, it is important to use this technique judiciously, as too many returns can make your code difficult to read and maintain.

**Additional Notes**

* **Early returns:** Early returns are returns that occur before the component's main return statement. These are typically used to conditionally prevent the rendering of the rest of the component.
* **Returning nothing:** Returning nothing is a way to conditionally prevent the rendering of a component or piece of JSX. This is often used when a condition is true and you do not want to render anything.

**Recommendation**

The recommendation for using conditional rendering is to use the return operator whenever you need to return some piece of JSX based on a condition. However, sometimes you may want to use multiple returns to return something entirely different, such as nothing or another component.

# Extracting JSX Into a New Component

**Creating and Using Components with Props**

**Extracting JSX into a New Component**

When the JSX in a component becomes too long, it is often helpful to extract parts of it into separate components. This makes the code more modular and easier to manage.

**Using Props to Pass Data Between Components**

Components can communicate with each other by passing data through props. Props are simply JavaScript objects that are passed from a parent component to a child component.

**Example:**

```jsx
// Footer.js
function Footer() {
  const openHour = 12;
  const closingHour = 22;

  return (
    <footer>
      <Order closingHour={closingHour} />
      <p>We're open until {closingHour}</p>
      <a href="#">Come visit us or order online!</a>
    </footer>
  );
}

// Order.js
function Order({ closingHour }) {
  return (
    <div className="order">
      <p>Open until {closingHour}</p>
      <button className="btn order">Order Now</button>
    </div>
  );
}
```

**Drawing Out the Componentry**

It can be helpful to draw out the componentry of a React application to get a better understanding of how the components work together. This can be done using a simple diagram or flowchart.

**Overall**

Creating and using components with props is an essential part of React development. This allows you to break down complex UIs into smaller, more manageable pieces and to pass data between components.

# Destructuring Props

**Destructuring Props in React Components**

**Introduction**

Destructuring is a JavaScript feature that allows us to extract values from nested objects and arrays. In React, we can use destructuring to extract props from the props object that is passed to a component. This can make our code more concise and easier to read.

**Example:**

```jsx
function Pizza({ pizza, soldOut }) {
  if (soldOut) {
    return null;
  }

  return (
    <li>
      <h3>{pizza.name}</h3>
      <p>Price: ${pizza.price}</p>
    </li>
  );
}
```

In this example, the Pizza component receives two props: pizza and soldOut. Instead of accessing these props using props.pizza and props.soldOut, we can destructure them directly into the component function parameters. This makes the code more concise and easier to read.

**Benefits of Destructuring Props**

* **Conciseness:** Destructuring props makes the code more concise by eliminating the need to use the props object repeatedly.
* **Readability:** Destructuring props makes the code more readable by making it clear which props are being used by the component.
* **Error Prevention:** Destructuring props can help prevent errors by making it clear which props are expected by the component.

**Tips for Destructuring Props**

* **Use curly braces:** Destructuring requires curly braces. Forgetting the curly braces will result in an error.
* **Destructure only the props you need:** Only destructure the props that are actually used by the component. Destructuring unused props can make the code more cluttered.
* **Handle missing props:** If a component may not receive a particular prop, use default values or conditional statements to handle the missing prop.

**Overall**

Destructuring props is a valuable technique for writing more concise, readable, and error-prone React code. By using destructuring, you can improve the maintainability and readability of your React components.

# React Fragments

**React Fragments**

**Introduction**

A React Fragment is a way to group multiple JSX elements together without adding an extra HTML element to the DOM. This can be useful when you want to render multiple elements without affecting the overall structure of your HTML.

**When to Use React Fragments**

There are a few situations where you might want to use React Fragments:

* When you want to render multiple JSX elements that would otherwise require a parent element.
* When you want to add a key to a list of JSX elements.
* When you want to improve the readability of your JSX code.

**Example Usage**

```jsx
<React.Fragment>
  <p>This is a paragraph.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</React.Fragment>
```

In this example, the React Fragment is used to group a paragraph and an unordered list together. This would be useful if you wanted to render these elements without adding an extra div element to the DOM.

**Adding a Key to a React Fragment**

If you need to add a key to a list of JSX elements that are rendered inside a React Fragment, you can use the following syntax:

```jsx
<React.Fragment key="some-key">
  <li>Item 1</li>
  <li>Item 2</li>
</React.Fragment>
```

This is useful for identifying individual elements in a list, especially when you are using maps or loops to render them.

**Alternative Syntax for React Fragments**

You can also use the following shorthand syntax for React Fragments:

```jsx
<>
  <p>This is a paragraph.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</>
```

This syntax is more concise and easier to type, but it does not support adding a key to the fragment.

**Overall**

React Fragments are a simple but versatile tool that can be used to improve the readability and maintainability of your JSX code. They are especially useful when you are rendering multiple elements that would otherwise require a parent element.

# Setting Classes and Text Conditionally

**Conditionally Setting Text and Class Names**

**Setting Text Content Conditionally**

To conditionally set the text content of an element, you can use a ternary operator within a JSX expression. For example:

```jsx
<span>{pizza.soldOut ? "Sold Out" : pizza.price}</span>
```

This code will display the text "Sold Out" if the pizza is sold out, or the pizza's price if it is not sold out.

**Setting Class Names Conditionally**

To conditionally set the class name of an element, you can use a template literal within a JSX expression. For example:

```jsx
<li className={`pizza ${pizza.soldOut ? "sold-out" : ""}`}>
  <h3>{pizza.name}</h3>
  <p>{pizza.price}</p>
</li>
```

This code will add the class "sold-out" to the LI element if the pizza is sold out. Otherwise, it will not add any class to the LI element.

**Advantages of Using Ternary Operators and Template Literals**

* **Clarity:** Ternary operators and template literals make your code more clear and easier to read.
* **Flexibility:** Ternary operators and template literals can be used to conditionally set a variety of properties, not just text content and class names.

**Overall**

Conditionally setting text content and class names is a common task in React development. By using ternary operators and template literals, you can write clean, readable, and flexible code.

# Section Summary

**Summary of Concepts Learned**

**Components**

* Components are the building blocks of React applications.
* Each component is a self-contained piece of the user interface.
* Components have their own data, JavaScript logic, and appearance.
* The appearance of a component is written using JSX.
* JSX can contain HTML, CSS, and JavaScript.

**Component Trees**

* A complete React application is composed of many different components.
* Components are organized into a tree structure.
* In a component tree, parent components include or use child components.
* A component can be a parent and a child at the same time.

**Props**

* Props are used to share data between components.
* Parent components pass props to child components.
* Props can only be passed down the component tree.

**Lists**

* Lists are created by rendering multiple components of the same type.
* Lists are created by looping over an array.
* The JavaScript map method is commonly used to create lists in React.

**Conditional Rendering**

* Conditional rendering is used to render components only when certain conditions are met.
* Common JavaScript tools used for conditional rendering include the ternary operator and multiple returns.

**Additional Concepts**

* Imperative vs. declarative programming
* Separation of concerns
* Immutability of props

