# Components, Instances, and Elements
### **React components, Component instances, and React elements**

**React components** are JavaScript functions or classes that describe a piece of the user interface. They return React elements, which are immutable objects that describe what should be rendered to the DOM.

**Component instances** are created when React renders a component. Each instance has its own state and props, and it goes through its own lifecycle.

**React elements** are the result of calling the `React.createElement()` function. They are immutable objects that describe what should be rendered to the DOM.

Here is a diagram that illustrates the relationship between these three concepts:

```
React component -> Component instance -> React element -> DOM element
```

### **Code examples**

**React component**

```javascript
const Button = (props) => {
  return <div onClick={props.onClick}>{props.children}</div>;
};
```

**Component instance**

```javascript
const buttonInstance = new Button({
  onClick: () => {
    console.log('Button clicked!');
  },
  children: 'Click me!',
});
```

**React element**

```javascript
const buttonElement = React.createElement(Button, {
  onClick: () => {
    console.log('Button clicked!');
  },
  children: 'Click me!',
});
```

**DOM element**

```html
<div onClick="console.log('Button clicked!')">Click me!</div>
```

### **How React renders components**

When React renders a component, it creates a component instance for each time the component is used in the code. Then, it calls the `render()` method on each instance, which returns a React element. Finally, React converts the React element to a DOM element and renders it to the screen.

### **Conclusion**

Understanding the difference between React components, component instances, and React elements is important for understanding how React works. It is also a common interview question.

I hope this explanation was helpful!

# Instances and Elements in Practice

### **React component instances and React elements in code**

**React component instances** are created when React renders a component. Each instance has its own state and props, and it goes through its own lifecycle.

**React elements** are the result of calling the `React.createElement()` function. They are immutable objects that describe what should be rendered to the DOM.

Here is an example of how to use React component instances and React elements in code:

```javascript
// React component instance
const buttonInstance = new Button({
  onClick: () => {
    console.log('Button clicked!');
  },
  children: 'Click me!',
});

// React element
const buttonElement = React.createElement(Button, {
  onClick: () => {
    console.log('Button clicked!');
  },
  children: 'Click me!',
});
```

**Calling components directly**

It is possible to call React components directly, but this is not recommended. When you call a component directly, React no longer sees it as a component instance, and instead sees it as the raw output element. This can lead to problems such as violating the rules of hooks.

Here is an example of how to call a component directly:

```javascript
// Call component directly
const tabContentElement = tabContent({
  item: {
    content: 'This is the content of the tab.',
  },
});
```

**Rendering components inside JSX**

The best way to render React components is inside JSX. This ensures that React sees the component as a component instance and not the raw output element.

Here is an example of how to render a component inside JSX:

```javascript
// Render component inside JSX
const tabContentElement = <tabContent item={{ content: 'This is the content of the tab.' }} />;
```

### **Conclusion**

It is important to understand the difference between React component instances and React elements. React component instances are created when React renders a component, and each instance has its own state and props. React elements are the result of calling the `React.createElement()` function, and they are immutable objects that describe what should be rendered to the DOM.

It is also important to note that you should never call React components directly. Instead, you should always render them inside JSX. This ensures that React sees the component as a component instance and not the raw output element.

# How Rendering Works: Overview

### **Summary of the React rendering process**

The React rendering process can be divided into three phases:

1. **Triggering a render:** A render can be triggered in two ways:
    * The initial render of the application.
    * A state update in one or more component instances.
2. **Render phase:** React calls the component functions and figures out how to update the DOM, but does not actually update the DOM in this phase.
3. **Commit phase:** React updates the DOM based on the results of the render phase.

**Triggering a render**

A render is triggered when the application starts up (initial render) or when a state update occurs (re-render). The render process is triggered for the entire application, not just for one single component.

**Render phase**

In the render phase, React calls the component functions and figures out how to update the DOM. However, React does not actually update the DOM in this phase. This is because React needs to know what the entire DOM should look like before it can start making changes.

**Commit phase**

In the commit phase, React updates the DOM based on the results of the render phase. This is where the actual visual changes to the user interface are made.

**Browser repaints the screen**

Once React has updated the DOM, the browser will notice the changes and repaint the screen. This is the final step in the rendering process, and it is not something that React is responsible for.

### **Additional details**

* Renders are not triggered immediately after a state update happens. Instead, they are scheduled for when the JavaScript engine has some free time on its hands.
* Multiple state updates in the same function will be batched, meaning that only one render will be triggered for all of the state updates.
* React looks at the entire component tree whenever a render happens, not just the component where the state update occurred. This is because React needs to know what the entire DOM should look like before it can start making changes.

I hope this summary is helpful!

# How Rendering Works: The Render Phase

The paragraph you provided does not contain any code, but I can still provide some detailed notes on the topic of React component communication.

## React component communication

React components can communicate with each other in a number of ways, including:

* **Props:** Props are one-way data flow from parent to child components.
* **State:** State is owned by the component that defines it, but it can be accessed by child components through props.
* **Context:** Context provides a way to share data between unrelated components without having to pass it down through props.
* **Refs:** Refs allow you to access the underlying DOM element of a component.
* **Callbacks:** Callbacks allow you to pass functions from parent to child components.

## Props

Props are the most common way for React components to communicate. Props are one-way data flow, meaning that data can only be passed from parent to child components.

Here is an example of how to use props to communicate between components:

```javascript
// Parent component
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Child count={count} />
    </div>
  );
}

// Child component
function Child({ count }) {
  return <div>{count}</div>;
}
```

In this example, the `Parent` component passes the `count` state variable to the `Child` component as a prop. The `Child` component then uses the `count` prop to display the current value of the counter.

## State

State is owned by the component that defines it, but it can be accessed by child components through props. This can be useful for creating complex components that need to share data between multiple levels of the component hierarchy.

Here is an example of how to use state to communicate between components:

```javascript
// Parent component
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Child count={count} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// Child component
function Child({ count }) {
  return <div>{count}</div>;
}
```

In this example, the `Parent` component defines the `count` state variable. The `Child` component then accesses the `count` state variable through the `count` prop. When the user clicks the "Increment" button, the `setCount` function is called, which increments the `count` state variable. This triggers a re-render of both the `Parent` and `Child` components, which will update the displayed value of the counter.

## Context

Context provides a way to share data between unrelated components without having to pass it down through props. This can be useful for sharing global data, such as the current user or theme.

Here is an example of how to use context to communicate between components:

```javascript
// Create a context object
const ThemeContext = createContext();

// Parent component
function Parent() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={theme}>
      <Child />
    </ThemeContext.Provider>
  );
}

// Child component
function Child() {
  const theme = useContext(ThemeContext);

  return <div>{theme}</div>;
}
```

In this example, the `Parent` component defines a `ThemeContext` context object and provides a value to it. The `Child` component then consumes the `ThemeContext` context object to access the current theme.

## Refs

Refs allow you to access the underlying DOM element of a component. This can be useful for interacting with the DOM directly, such as focusing an input element or scrolling to a specific element.

Here is an example of how to use refs to communicate between components:

```javascript
// Parent component
function Parent() {
  const inputRef = useRef();

  function focusInput() {
    inputRef.current.focus();
  }

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus input</button>
    </div>
  );
}
```

In this example, the `Parent` component creates a ref to the input element and stores it in the `inputRef` variable. The `focusInput` function then uses

# How Rendering Works: The Commit Phase

**Detailed notes with code from the paragraph given:**

**Overview of the React rendering process**

The React rendering process can be divided into two main phases: the render phase and the commit phase.

**Render phase**

The render phase is responsible for creating a new virtual DOM tree, which is a representation of the desired state of the UI. React uses a diffing algorithm to compare the new virtual DOM tree to the current fiber tree, which is a representation of the current state of the UI. This allows React to identify the smallest set of DOM updates that are necessary to bring the UI into sync with the new virtual DOM tree.

**Commit phase**

The commit phase is responsible for applying the DOM updates that were identified in the render phase. React does this by calling a renderer, such as React DOM, which is responsible for interacting with the specific platform on which the React app is running.

**Code example**

The following code example shows a simple React component that renders a button:

```javascript
import React from 'react';

const Button = () => {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <button onClick={handleClick}>Click me {count} times</button>
  );
};

export default Button;
```

When the user clicks the button, the `handleClick()` function is called, which increments the `count` state variable. This causes React to trigger a re-render of the component.

During the render phase, React will create a new virtual DOM tree that reflects the updated state of the component. React will then compare the new virtual DOM tree to the current fiber tree and identify the smallest set of DOM updates that are necessary to bring the UI into sync.

In this case, the only DOM update that is necessary is to update the text of the button to reflect the new value of the `count` state variable.

During the commit phase, React will call the renderer to apply the DOM update. The renderer will then update the text of the button on the screen.

**Additional notes**

* The render phase is asynchronous, which means that React can prioritize and split work into chunks, and pause and resume some work later. This is necessary for concurrent features and also to prevent the JavaScript engine from being blocked by complex render processes.
* The commit phase is synchronous, which means that all of the DOM updates are performed in one go. This is necessary to ensure a consistent UI over time.
* React apps can be built without being aware of most of the details of the rendering process. However, it is helpful to have a basic understanding of how the process works in order to troubleshoot performance issues and to understand the implications of different design decisions.

# How Diffing Works 
**Detailed notes with code from the paragraph given:**

## Diffing Algorithm in React

### Overview

The diffing algorithm in React is responsible for comparing two DOM trees and identifying the smallest set of DOM updates that are necessary to bring the current DOM tree into sync with the desired DOM tree. This algorithm is based on two fundamental assumptions:

1. Two elements of different types will produce different trees.
2. Elements with a stable key will stay the same across renders.

### Two Different Elements at the Same Position

If the diffing algorithm finds two different elements at the same position in the tree between two renders, React will assume that the element itself plus all its children are no longer valid. Therefore, all these elements will be destroyed and removed from the DOM. This includes their state as well.

```javascript
// Before
const element = <div><SearchBar /></div>;

// After
const element = <header><ProfileMenu /></header>;

// The <SearchBar /> component will be destroyed and removed from the DOM.
```

### Same Element at the Same Position

If the diffing algorithm finds the same element at the same position in the tree between two renders, React will simply keep the element in the DOM. This includes all child elements and, more importantly, the component's state.

```javascript
// Before
const element = <div><SearchBar /></div>;

// After
const element = <div><SearchBar /></div>;

// The <SearchBar /> component will be kept in the DOM.
```

### Attribute Updates

If the diffing algorithm finds that the element type has not changed, but some of the element's attributes have changed, React will simply mutate the DOM element attributes. In the case of React elements, it will pass in the new props.

```javascript
// Before
const element = <div className="my-class"><SearchBar /></div>;

// After
const element = <div className="my-other-class"><SearchBar /></div>;

// The DOM element attribute will be updated from `my-class` to `my-other-class`.
```

### Key Prop

The key prop is a way to tell React that an element should be preserved across renders, even if its type or attributes have changed. This is useful for components that have state, as it allows React to keep track of the state and avoid recreating the component unnecessarily.

```javascript
// Before
const element = <ul><li>Item 1</li><li>Item 2</li></ul>;

// After
const element = <ul><li key="1">Item 1</li><li key="2">Item 2</li></ul>;

// The <li> elements will be kept in the DOM, even though their keys have changed.
```

## Conclusion

The diffing algorithm in React is a powerful tool that allows for efficient updates to the DOM. By understanding how the diffing algorithm works, you can write React components that are performant and maintainable.

# Diffing Rules in Practice

**Detailed notes with code from the paragraph given:**

**Diffing rules in action**

In the paragraph given, the author is demonstrating how the diffing rules in React work in practice. They use a simple tab component to illustrate how the state of a component is preserved across renders when the component instance remains in the same position in the tree.

**Code example**

The following code example shows the tab component that the author uses in the paragraph:

```javascript
import React from 'react';

const Tab = ({ tabNum, onTabChange }) => {
  const [isHidden, setIsHidden] = React.useState(true);
  const [likes, setLikes] = React.useState(4);

  const handleLikeClick = () => {
    setLikes(likes + 1);
  };

  const handleHideClick = () => {
    setIsHidden(true);
  };

  if (tabNum === 3) {
    return <DifferentContent />;
  }

  return (
    <div>
      <h1>Tab {tabNum}</h1>
      <button onClick={handleHideClick}>Hide details</button>
      {!isHidden && <p>This is the content for tab {tabNum}.</p>}
      <button onClick={handleLikeClick}>Likes: {likes}</button>
    </div>
  );
};

export default Tab;
```

**Explanation**

When the user clicks on a tab, the tab component is re-rendered. However, the component instance remains in the same position in the tree. This means that the state of the component is preserved across renders.

The author demonstrates this by clicking on the different tabs and showing how the state of the component (the hidden state and the likes count) remains the same.

The author also shows how the state of the component is reset when the component instance is replaced. For example, when the user clicks on tab 4, the tab content component is replaced with a different content component. As a result, the state of the tab content component is reset.

**Conclusion**

The diffing rules in React are important to understand because they have a practical effect on how React applications work. By understanding how the diffing rules work, you can write React components that are performant and maintainable.


# The Key Prop

**Detailed notes with code from the paragraph given:**

**Key prop in React**

The key prop in React is a way to tell the diffing algorithm that a certain element is unique. This works for both DOM elements and React elements.

**When to use the key prop**

There are two main use cases for the key prop:

1. **To improve performance in lists:** When you have a list of elements, React will use the key prop to identify which elements have moved and which elements have stayed the same. This allows React to update the DOM more efficiently.
2. **To reset state in component instances:** If you have a component instance that needs to reset its state when its props change, you can use the key prop to tell React to create a new component instance instead of updating the existing one.

**Code example**

The following code example shows how to use the key prop in a list:

```javascript
const listItems = [
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
];

return (
  <ul>
    {listItems.map((item) => (
      <li key={item.id}>{item.name}</li>
    ))}
  </ul>
);
```

In this example, React will use the `id` prop of each item to identify it. This allows React to efficiently update the DOM when items are added, removed, or moved.

**Code example**

The following code example shows how to use the key prop to reset state in a component instance:

```javascript
class Question extends React.Component {
  state = {
    answer: '',
  };

  render() {
    return (
      <div>
        <p>Question: {this.props.question}</p>
        <input type="text" value={this.state.answer} />
      </div>
    );
  }
}

function App() {
  const [question, setQuestion] = React.useState('What is the capital of France?');

  return (
    <div>
      <Question key={question} question={question} />
    </div>
  );
}
```

In this example, the `Question` component instance will reset its state when the `question` prop changes. This is because React will create a new component instance with a different key.

**Conclusion**

The key prop is an important tool for improving performance and managing state in React applications. It is important to understand how to use the key prop correctly in order to write efficient and maintainable code.

# Resetting State With the Key Prop

**Detailed notes with code from the paragraph given:**

**Using the key prop to reset state in a tabbed component**

In the paragraph given, the author shows how to use the key prop to reset state in a tabbed component.

**Code example**

The following code example shows how to use the key prop to reset state in a tabbed component:

```javascript
class TabContent extends React.Component {
  state = {
    isHidden: true,
    likes: 0,
  };

  render() {
    const { content } = this.props;

    return (
      <div>
        <h1>{content.title}</h1>
        <button onClick={() => this.setState({ isHidden: true })}>
          Hide details
        </button>
        {!this.state.isHidden && <p>{content.summary}</p>}
        <button onClick={() => this.setState({ likes: this.state.likes + 1 })}>
          Likes: {this.state.likes}
        </button>
      </div>
    );
  }
}

function App() {
  const [currentTab, setCurrentTab] = React.useState(0);
  const tabs = [
    {
      title: 'Tab 1',
      content: {
        summary: 'This is the content for tab 1.',
      },
    },
    {
      title: 'Tab 2',
      content: {
        summary: 'This is the content for tab 2.',
      },
    },
  ];

  return (
    <div>
      <ul>
        {tabs.map((tab, index) => (
          <li key={index} onClick={() => setCurrentTab(index)}>
            {tab.title}
          </li>
        ))}
      </ul>
      <TabContent key={currentTab} content={tabs[currentTab]} />
    </div>
  );
}
```

In this example, the `TabContent` component has a key prop that is set to the current tab index. This means that each time the tab changes, the `TabContent` component will be re-rendered with a different key.

As a result, React will treat the `TabContent` component as a new instance and reset its state.

This is exactly what we want, because we want the state of the `TabContent` component to be reset when the tab changes.

**Conclusion**

The key prop is a powerful tool for resetting state in React components. By using the key prop correctly, you can write efficient and maintainable code.

# Using the Key Prop to Fix Our Eat-'N-Split App

## Notes on how to fix the remaining problem in the Eat-'N-Split app

**Problem:** The bill value is not reset when moving from one friend to another.

**Solution:** Make each component instance unique by providing a key that changes across the re-renders.

**Steps:**

1. Identify the component where the problem is occurring. In this case, it is the `FormSplitBill` component.
2. Find where the component is being used in the app.
3. Add a `key` prop to the component and pass a unique value to it. In this case, we can use the `selectedfriend.id`.

**Code:**

```javascript
// FormSplitBill.js
const FormSplitBill = ({ selectedfriend }) => {
  return (
    <form>
      <input type="number" placeholder="Bill amount" />
      <button type="submit">Split bill</button>
    </form>
  );
};

// App.js
import FormSplitBill from './FormSplitBill';

const App = () => {
  const [selectedFriend, setSelectedFriend] = useState(null);

  return (
    <div>
      <h1>Eat-'N-Split</h1>
      <FormSplitBill key={selectedFriend?.id} selectedfriend={selectedFriend} />
    </div>
  );
};
```

**Explanation:**

The `key` prop tells React which component instance is which. When the `key` prop changes, React treats the component as a new instance. This is why the bill value is reset when moving from one friend to another in the example above.

## Tips for choosing unique keys

* Use a unique identifier, such as an ID from a database.
* Avoid using non-unique values, such as indexes or random numbers.
* If you are rendering a list of components, you can use the index of the item in the list as the key. However, this is not ideal, as it can lead to performance problems if the list is reordered.

## Conclusion

By adding a `key` prop to the `FormSplitBill` component and passing a unique value to it, we were able to fix the problem of the bill value not being reset when moving from one friend to another.

# Rules for Render Logic: Pure Components
## Notes on render logic in React

**What is render logic?**

Render logic is the code that determines what is displayed on the screen. It is the code that is executed by the `render()` method of a React component.

**Differences between render logic and event handler functions**

Event handler functions are functions that are executed when a user interacts with the UI, such as clicking a button or typing in an input field. Render logic, on the other hand, is code that is executed independently of user interactions.

**Rules for render logic**

* Render logic should be pure. This means that it should not modify any state, and it should always return the same result for the same inputs.
* Render logic should be declarative. This means that it should describe what should be rendered, rather than how it should be rendered.
* Render logic should be side-effect free. This means that it should not perform any operations that change the outside world, such as making network requests or writing to the DOM.

**Code example**

The following code shows an example of a simple React component with render logic:

```javascript
function MyComponent({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

The render logic in this component is pure, declarative, and side-effect free. It simply returns a heading element with the name of the user passed in as a prop.

**Best practices for render logic**

* Use components to organize your render logic. This will make your code more reusable and maintainable.
* Use conditional rendering to display different content based on the state of your application.
* Use loops to render lists of items.
* Use refs to access DOM elements.

**Conclusion**

By following these simple rules, you can write clean and efficient render logic in React.

# State Update Batching
**Summary of notes on state update batching in React**

* React batches state updates in the same event handler function into a single state update. This means that React will only trigger a single render and commit, even if multiple state variables are updated.
* State updates are asynchronous, meaning that the updated state variable is not available immediately after the setState call, but only after the re-render has happened.
* Prior to React 18, automatic batching was only done in event handlers. In React 18 and later, automatic batching is done for all state updates, regardless of where they are called.
* There are some extremely rare situations in which automatic batching can be problematic. In these cases, you can wrap the problematic state update in a ReactDOM.flushSync function to exclude it from batching.

**Example code**

```javascript
function MyComponent() {
  const [answer, setAnswer] = useState('');
  const [best, setBest] = useState('');
  const [solved, setSolved] = useState(false);

  function reset() {
    setAnswer('');
    setBest('');
    setSolved(false);

    // The answer state variable will still hold the current state
    // at this point, even though we have already told React to update it.
    console.log(answer); // ''
  }

  // ...
}
```

**Conclusion**

State update batching is a powerful performance optimization that React provides out of the box. It is important to understand how batching works so that you can write efficient React code.

# State Update Batching in Practice

**Summary of notes on state update batching in React**

**What is state update batching?**

State update batching is a performance optimization that React uses to reduce the number of times the component re-renders. When multiple state updates are performed in a short period of time, React will batch them together and only re-render the component once.

**When does state update batching happen?**

State update batching happens in the following situations:

* In React 18 and later, state update batching happens for all state updates, regardless of where they are called.
* In React 17 and earlier, state update batching only happened for state updates called inside of event handlers.

**How to use state update batching**

To use state update batching, you simply need to call the `setState()` function multiple times in a short period of time. React will automatically batch the state updates together and only re-render the component once.

**Why is state update batching important?**

State update batching is important because it can improve the performance of your React applications. By reducing the number of re-renders, state update batching can make your applications more responsive and fluid.

**Example code**

```javascript
// This code will only cause the component to re-render once
const [count, setCount] = useState(0);

function handleClick() {
  setCount(count + 1);
  setCount(count + 1);
}
```

**Best practices for state update batching**

Here are some best practices for using state update batching:

* Use state update batching whenever you need to update multiple state variables in a short period of time.
* If you are using React 17 or earlier, make sure to call your state update functions inside of event handlers to ensure that they are batched.
* If you need to update state based on the current state, use a callback function instead of just a value.

**Conclusion**

State update batching is a powerful performance optimization that React provides out of the box. By understanding how batching works and following the best practices above, you can write efficient and performant React code.

# How Events Work in React
**Summary of notes on React event delegation and synthetic events**

**React event delegation**

React implements event delegation for all events in your application. This means that all events are delegated to the root DOM container, where they are handled by React. This is more performant than attaching event handlers to each individual element.

**Synthetic events**

When you declare an event handler in React, you get access to a synthetic event object. Synthetic events are wrappers around the native DOM event object. They have the same interface as native event objects, but they also fix some browser inconsistencies and make all of the most important synthetic events bubble.

**Differences between React and vanilla JavaScript event handlers**

* In React, event handler props are named using camelCase, e.g. `onClick`. In HTML, they are named using lowercase, e.g. `onclick`. In vanilla JavaScript, they are named using lowercase without the `on` prefix, e.g. `click`.
* In React, to stop the default behavior of the browser in response to an event, you can call the `preventDefault()` method on the event object. In vanilla JavaScript, you can return `false` from the event handler function.

**Example code**

```javascript
// React
const onClick = (event) => {
  // Prevent the default behavior of the browser
  event.preventDefault();
};

function Button() {
  return <button onClick={onClick}>Click me!</button>;
}

// Vanilla JavaScript
const button = document.querySelector('button');

button.addEventListener('click', () => {
  // Prevent the default behavior of the browser
  event.preventDefault();
});
```

**Conclusion**

React event delegation and synthetic events are powerful features that make it easy to write efficient and performant React code. By understanding how they work, you can write more robust and maintainable applications.

# Libraries vs. Frameworks & The React Ecosystem

## Summary of notes on the difference between React frameworks and libraries

**Frameworks**

* A framework is a complete structure that includes everything you need to build a complete large-scale application.
* Frameworks are batteries included, meaning they come with everything you need out of the box, such as routing, styling, HTTP requests, and more.
* The downside of frameworks is that you're stuck with the framework's tools and conventions, even if you don't like or agree with them.
* Examples of React frameworks include Next.js, Remix, and Gatsby.

**Libraries**

* A library is a piece of code that developers share for other developers to use.
* React is a view library, meaning it only draws components onto a user interface.
* To build a large-scale single page application with React, you'll need to include many external third-party libraries for things like routing, styling, HTTP requests, and so on.
* The benefit of using libraries is that you have incredible freedom to choose exactly the ones that you like the most and that are specific to your application's needs.
* Examples of React libraries include React Router, React Query, Redux, styled-components, and Tailwind CSS.

**Which one should I use?**

If you're new to React, it's generally recommended to start with a library. This will allow you to learn the core concepts of React without having to worry about making decisions about which libraries to use.

Once you have a good understanding of React, you can then consider using a framework. Frameworks can make it much easier and faster to build large-scale React applications, but they can also be more complex to learn and use.

**Here is a table that summarizes the key differences between React frameworks and libraries:**

| Feature | Framework | Library |
|---|---|---|
| Completeness | Complete structure with everything you need to build a large-scale application | Not complete, you need to include additional libraries |
| Tools and conventions | Fixed set of tools and conventions | Flexible, you can choose the tools and conventions that you like the most |
| Examples | Next.js, Remix, Gatsby | React Router, React Query, Redux, styled-components, Tailwind CSS |

**Conclusion**

The best choice for you will depend on your specific needs and experience level. If you're new to React, start with a library. Once you have a good understanding of React, you can then consider using a framework.

# Practical Takeaways

**Key takeaways from the last lecture of the section:**

* **Components:** A component is a blueprint for a piece of UI, and a component instance is a physical manifestation of a component. When a component instance is rendered, it returns a React element.
* **Rendering:** Rendering in React is the process of calling component functions and calculating which dumb elements need to be inserted, deleted, or updated later. It does not involve actually writing to the DOM.
* **Re-rendering:** A component instance re-renders when its state changes or when one of its parent components re-renders.
* **Reconciliation:** Reconciliation is the process by which React compares the current DOM tree to the desired DOM tree and updates the DOM as efficiently as possible.
* **Diffing:** Diffing is a key part of reconciliation. It is the process by which React decides which dumb elements need to be added or modified.
* **Keys:** Keys are a way to uniquely identify React elements. They are useful for preventing unnecessary recreations of elements in the DOM, especially in lists.
* **Nesting components:** It is best to avoid nesting components, as this can lead to performance problems and state management issues.
* **Render logic:** Render logic is the logic that is responsible for creating DOM elements. It should not contain any side effects.
* **Side effects:** Side effects are actions that can change something outside of the component, such as making an API call or updating the DOM. Side effects are only allowed inside event handlers and inside useEffect.
* **Committing:** Committing is the process of updating the DOM. It is done by ReactDOM, not React.
* **Batching state updates:** React batches state updates, meaning that multiple state updates will be applied to the component all at once. This improves performance by minimizing the number of re-renders.
* **Asynchronous state updates:** State updates are asynchronous, meaning that a state variable may not be updated immediately after we update it.
* **Synthetic events:** React uses synthetic event objects instead of native browser event objects. This ensures that events work the same way across all browsers.
* **React is a library:** React is a library, not a framework. This means that you have the flexibility to choose the third-party libraries that you want to use with React.

**Additional notes:**

* To prevent state management issues, it is best to declare new components at the top level of a file, never inside another component.
* The most commonly used React libraries will be covered in the main projects of the course.
