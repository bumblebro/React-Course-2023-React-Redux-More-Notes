# What is "Thinking in React"?

**Notes on React mindset:**

* **Mental model of React tools:** components, state, props, data flow, effects, etc.
* **Thinking in terms of state transitions rather than element mutations.**
* **Component tree:** how components are related to each other.
* **Reusability and composability of components.**
* **Static version of the application:** without state and interactivity.
* **State management:** deciding when to use state, what types of state to use, and where to place each piece of state.
* **Data flow:** one-way data flow, child-to-parent communication, and the way global state should be accessed.

**Code examples:**

```javascript
// Component tree
const App = () => {
  return (
    <div>
      <Header />
      <Content />
      <Footer />
    </div>
  );
};

const Header = () => {
  return <h1>My React App</h1>;
};

const Content = () => {
  return <p>This is the content of my React app.</p>;
};

const Footer = () => {
  return <p>Copyright © 2023 My Name</p>;
};
```

```javascript
// State management
const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

```javascript
// Data flow
const Parent = () => {
  const [state, setState] = useState({
    name: 'John Doe',
  });

  return (
    <div>
      <Child state={state} />
    </div>
  );
};

const Child = ({ state }) => {
  const [name, setName] = useState(state.name);

  return (
    <div>
      <p>My name is {name}</p>
      <button onClick={() => setName('Jane Doe')}>Change name</button>
    </div>
  );
};
```

# Fundamentals of State Management

**Notes on state management in React:**

* **Local state:** State that is only needed in one component or a few different components.
* **Global state:** State that many different components in the app might need access to.

**Decision process for when to create state:**

1. **Does the data change at some point in time?**
    * If yes, then create a new piece of state using the `useState` function.
    * If no, then you only need a regular variable.
2. **Can the new data be computed from an existing piece of state or props?**
    * If yes, then derive the state.
    * If no, then create a new piece of state.

**Decision process for where to place state:**

1. **Is the state only used by the current component?**
    * If yes, then leave it in the current component.
2. **Is the state also necessary for a child component?**
    * If yes, then pass the state down to the child component using props.
3. **Is the state also necessary for sibling components or a parent component?**
    * If yes, then lift the state up to the first common parent component.
4. **Is the state necessary for many different components all over the app?**
    * If yes, then this is global state.

**Example flow chart:**

```
Does the data change at some point in time?
  Yes
    Is the new data computable from an existing piece of state or props?
      Yes
        Derive the state
      No
        Create a new piece of state
  No
    Create a regular variable

Where is the state needed?
  Only in the current component
    Leave the state in the current component
  Also in a child component
    Pass the state down to the child component using props
  Also in sibling components or a parent component
    Lift the state up to the first common parent component
  Necessary for many different components all over the app
    Global state
```

**Benefits of using local state:**

* It is easier to reason about and manage.
* It is more performant.
* It is more scalable.

**When to use global state:**

* When the state is needed by many different components all over the app.
* When the state is complex and difficult to manage with local state.

**Conclusion:**

State management is an important aspect of React development. By following the guidelines in this section, you can make better decisions about when to create state and where to place it. This will lead to more maintainable and scalable React applications.

# Thinking About State and Lifting State Up

**Notes from the paragraph:**

* **What is lifting state up?**

Lifting state up is a technique in React for moving state from a child component to its closest common parent component. This is done when multiple sibling components need to access the same state.

* **Why do we lift state up?**

Lifting state up has several benefits:

    * It prevents duplicate state from being stored in multiple components.
    * It makes the state more central and easier to manage.
    * It makes it easier to share state between sibling components.

* **How to lift state up**

To lift state up, we follow these steps:

    1. Move the state variable to the closest common parent component.
    2. Pass the state variable as a prop to the child components that need it.
    3. Update the child components to use the state prop instead of their own local state.

**Example from the paragraph:**

In the example from the paragraph, we have a form component and a packing list component. Both components need to access the state of the packing items. However, the form component is only responsible for adding new items to the packing list, while the packing list component is responsible for rendering the items.

Therefore, we lift the packing items state up to the app component, which is the closest common parent of the form component and the packing list component. We then pass the packing items state as a prop to both components.

**Code from the paragraph:**

```javascript
// App component
const App = () => {
  const [items, setItems] = useState([]);

  const handleAddItems = (newItem) => {
    setItems([...items, newItem]);
  };

  return (
    <div>
      <Form onAddItems={handleAddItems} />
      <PackingList items={items} />
    </div>
  );
};

// Form component
const Form = ({ onAddItems }) => {
  const handleSubmit = (event) => {
    event.preventDefault();

    const newItem = {
      // ...
    };

    onAddItems(newItem);
  };

  return (
    <form onSubmit={handleSubmit}>
      // ...
    </form>
  );
};

// PackingList component
const PackingList = ({ items }) => {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>{item.description}</li>
      ))}
    </ul>
  );
};
```

## Conclusion

Lifting state up is an important technique to learn in React. It allows you to manage state more effectively and share state between sibling components.

# Reviewing "Lifting Up State"

**Notes from the paragraph:**

* **Why do we need to lift state up?**

We need to lift state up when we need to share state between sibling components. This is because React has one-way data flow, so data can only flow down from parents to children.

* **How to lift state up**

To lift state up, we follow these steps:

    1. Move the state variable to the closest common parent component.
    2. Pass the state variable as a prop to the child components that need it.
    3. Update the child components to use the state prop instead of their own local state.

* **What is child-to-parent communication?**

Child-to-parent communication is a technique for allowing child components to update state that lives in the parent component. This is done by passing down a setter function from the parent component to the child component. The child component can then use the setter function to update the parent state.

* **Example**

In the example from the paragraph, we have a checkout component with two child components: promotions and total. The promotions component needs to be able to update the coupon state, which lives in the checkout component.

To do this, we first lift the coupon state up to the checkout component. Then, we pass down a setter function, setCoupons, to the promotions component. The promotions component can then use setCoupons to update the coupon state.

**Code from the paragraph:**

```javascript
// Checkout component
const Checkout = () => {
  const [coupons, setCoupons] = useState([]);

  return (
    <div>
      <Promotions setCoupons={setCoupons} />
      <Total coupons={coupons} />
    </div>
  );
};

// Promotions component
const Promotions = ({ setCoupons }) => {
  const handleAddCoupon = (event) => {
    event.preventDefault();

    const newCoupon = {
      // ...
    };

    setCoupons([...coupons, newCoupon]);
  };

  return (
    <form onSubmit={handleAddCoupon}>
      // ...
    </form>
  );
};

// Total component
const Total = ({ coupons }) => {
  // ...
};
```

## Conclusion

Lifting state up and child-to-parent communication are important techniques to learn in React. They allow you to share state between sibling components and update state from child components. These techniques are essential for building complex React applications.

# Deleting an Item: More Child-to-Parent Communication!
**Notes from the paragraph:**

* **What is the goal of this paragraph?**

The goal of this paragraph is to explain how to implement child-to-parent communication in order to delete items from a list in React.

* **How to implement child-to-parent communication**

To implement child-to-parent communication, we follow these steps:

    1. Create a function in the parent component that will handle the update to the state.
    2. Pass the function as a prop to the child component.
    3. Call the function in the child component when the desired event happens.

* **Example**

In the example from the paragraph, we have an app component with a packing list component. The packing list component has an item component for each item in the list.

We want to be able to delete items from the list by clicking on a cross next to each item. To do this, we will implement child-to-parent communication.

First, we create a function in the app component called handleDeleteItem. This function will take an ID as an argument and remove the corresponding item from the state.

```javascript
const App = () => {
  const [items, setItems] = useState([]);

  const handleDeleteItem = (id) => {
    setItems(items.filter((item) => item.id !== id));
  };

  return (
    <PackingList items={items} onDeleteItem={handleDeleteItem} />
  );
};
```

Next, we pass the handleDeleteItem function as a prop to the packing list component.

```javascript
const PackingList = ({ items, onDeleteItem }) => {
  return (
    <ul>
      {items.map((item) => (
        <Item key={item.id} item={item} onDeleteItem={onDeleteItem} />
      ))}
    </ul>
  );
};
```

Finally, we call the handleDeleteItem function in the item component when the cross is clicked.

```javascript
const Item = ({ item, onDeleteItem }) => {
  return (
    <li>
      {item.name}
      <button onClick={() => onDeleteItem(item.id)}>X</button>
    </li>
  );
};
```

Now, when we click on the cross next to an item, the handleDeleteItem function will be called and the item will be removed from the state.

## Conclusion

Child-to-parent communication is a powerful technique that allows us to update state from child components. This is essential for building complex React applications.

# Updating an Item: Complex Immutable Data Operation
**Notes from the paragraph:**

* **What is the goal of this paragraph?**

The goal of this paragraph is to explain how to implement child-to-parent communication in order to toggle the packed status of items in a list in React.

* **How to implement child-to-parent communication**

To implement child-to-parent communication, we follow these steps:

    1. Create a function in the parent component that will handle the update to the state.
    2. Pass the function as a prop to the child component.
    3. Call the function in the child component when the desired event happens.

* **How to toggle the packed status of an item**

To toggle the packed status of an item, we can use the following steps:

    1. Create a new array from the current array, where the packed status of the item with the specified ID is toggled.
    2. Set the state to the new array.

* **Code from the paragraph:**

```javascript
// App component
const App = () => {
  const [items, setItems] = useState([]);

  const toggleItem = (id) => {
    setItems(items.map((item) => {
      if (item.id === id) {
        return { ...item, packed: !item.packed };
      } else {
        return item;
      }
    }));
  };

  return (
    <PackingList items={items} onToggleItem={toggleItem} />
  );
};

// PackingList component
const PackingList = ({ items, onToggleItem }) => {
  return (
    <ul>
      {items.map((item) => (
        <Item key={item.id} item={item} onToggleItem={onToggleItem} />
      ))}
    </ul>
  );
};

// Item component
const Item = ({ item, onToggleItem }) => {
  return (
    <li>
      <input
        type="checkbox"
        checked={item.packed}
        onChange={() => onToggleItem(item.id)}
      />
      {item.name}
    </li>
  );
};
```

## Conclusion

Child-to-parent communication and toggling the packed status of an item are important concepts in React. By understanding these concepts, you will be able to build more complex and interactive React applications.
# Derived State

**Notes from the paragraph:**

* **What is derived state?**

Derived state is state that is computed from another existing piece of state or props.

* **Why use derived state?**

There are two main benefits to using derived state:

    1. **Reduces complexity:** Derived state can reduce the complexity of your code by eliminating the need to manage multiple state variables that are dependent on each other.
    2. **Improves performance:** Derived state can improve performance by avoiding unnecessary re-renders. When you update a piece of derived state, React will only re-render the component if the value of the derived state has actually changed.

* **Example**

In the example from the paragraph, we have three state variables: cart, numItems, and totalPrice. However, numItems and totalPrice can be easily computed from the cart state variable.

```javascript
// Without derived state:
const [cart, setCart] = useState([]);
const [numItems, setNumItems] = useState(0);
const [totalPrice, setTotalPrice] = useState(0);

// Update the cart state:
setCart([...cart, { name: 'Item 1', price: 10 }]);

// Update the numItems and totalPrice state variables manually:
setNumItems(numItems + 1);
setTotalPrice(totalPrice + 10);
```

This code is complex and error-prone. We need to be careful to always update the numItems and totalPrice state variables whenever we update the cart state variable. Otherwise, our states will get out of sync.

```javascript
// With derived state:
const [cart, setCart] = useState([]);
const numItems = cart.length;
const totalPrice = cart.reduce((sum, item) => sum + item.price, 0);

// Update the cart state:
setCart([...cart, { name: 'Item 1', price: 10 }]);
```

This code is much simpler and more robust. We don't need to manually update the numItems and totalPrice state variables. Instead, they are derived from the cart state variable automatically.

## Conclusion

Derived state is a powerful technique that can help you to write simpler, more robust, and more performant React code. Whenever you have a situation where one state variable can be easily computed from another, always prefer derived state.

# Calculating Statistics as Derived State

**Notes from the paragraph:**

* **What is derived state?**

Derived state is state that is computed from existing state or props.

* **Why use derived state?**

Derived state has several benefits, including:

    * It reduces complexity by eliminating the need to manage multiple state variables that are dependent on each other.
    * It improves performance by avoiding unnecessary re-renders.
    * It makes code more readable and maintainable.

* **Example**

In the example from the paragraph, we want to calculate the number of items on the list, how many we have already packed, and the percentage of that. We can use derived state to compute these values from the `items` state variable.

```javascript
// Derived state:
const numItems = items.length;
const packedItems = items.filter(item => item.packed);
const percentagePacked = (packedItems.length / numItems) * 100;
```

We can then use these derived state variables in our component's render method.

```javascript
// Render method:
<span>
  You have {numItems} items on your list, {packedItems.length} of which are packed
  ({percentagePacked}% packed).
</span>
```

* **Early returns**

An early return is a conditional statement that returns from a function early if a certain condition is met. This can be useful for simplifying code and making it more readable.

In the example from the paragraph, we want to display a different message if the user has no items on their list. We can use an early return to avoid performing unnecessary calculations.

```javascript
// Render method:
if (!items.length) {
  return <p className="footer">Start adding some items to your packing list! 🚀</p>;
}

// ...
```

## Conclusion

Derived state and early returns are two powerful techniques that can help you to write better React code. By using these techniques, you can reduce complexity, improve performance, and make your code more readable and maintainable.

# Sorting Items

**Notes from the paragraph:**

* **Feature:** Allow users to sort the items in the packing list by three different criteria: input order, description, and packed status.
* **Implementation:**
    1. Create a new piece of state called `sortBy` to track the currently selected sort criteria.
    2. Create a new derived state variable called `sortedItems` to store the items sorted by the currently selected sort criteria.
    3. Use the `sortedItems` variable to render the items in the packing list.

**Code:**

```javascript
// State:
const [sortBy, setSortBy] = useState('input');

// Derived state:
const sortedItems = sortBy === 'input'
  ? items
  : sortBy === 'description'
    ? items.slice().sort((a, b) => a.description.localeCompare(b.description))
    : items.slice().sort((a, b) => a.packed - b.packed);

// Render:
<ul>
  {sortedItems.map((item) => (
    <li key={item.id}>{item.description}</li>
  ))}
</ul>
```

**Benefits of using derived state:**

* **Reduced complexity:** We don't need to create a new state variable for the sorted items. Instead, we can simply compute them from the existing `items` state variable. This makes our code simpler and easier to maintain.
* **Improved performance:** We can avoid unnecessary re-renders by only re-calculating the sorted items whenever the `sortBy` state variable changes.

## Conclusion

Derived state is a powerful technique that can help us to write simpler, more performant, and more maintainable React code. It is especially useful for computing values that can be easily computed from other state variables.

# Clearing the List

**Notes on adding a button to clear up the entire list in React:**

To add a button to clear up the entire list in React, we can follow these steps:

1. Create a function to clear the list. This function should set the list state back to the original value, which is an empty array.
2. Pass this function to the button as an onClick prop.
3. Add a confirmation message to prevent the user from accidentally deleting everything.

**Code:**

```javascript
// Create a function to clear the list.
function handleClearList() {
  setItems([]);
}

// Pass the function to the button as an onClick prop.
<button onClick={handleClearList}>Clear list</button>

// Add a confirmation message to prevent the user from accidentally deleting everything.
const confirmed = window.confirm('Are you sure you want to delete all items?');

if (confirmed) {
  setItems([]);
}
```

**Example:**

```javascript
import React, { useState } from 'react';

const PackingList = () => {
  const [items, setItems] = useState(['shorts', 'charger']);

  function handleClearList() {
    setItems([]);
  }

  return (
    <ul>
      {items.map((item) => (
        <li key={item}>{item}</li>
      ))}
      <button onClick={handleClearList}>Clear list</button>
    </ul>
  );
};

export default PackingList;
```

**Output:**

```html
<ul>
  <li>shorts</li>
  <li>charger</li>
  <button>Clear list</button>
</ul>
```

When the user clicks the "Clear list" button, they will be prompted with a confirmation message. If they click "Okay", the list will be cleared.

# Moving Components Into Separate Files

**Notes on splitting the App.js file into multiple component files:**

To split the App.js file into multiple component files, we can follow these steps:

1. Identify the different components in the App.js file.
2. Create a new file for each component.
3. Cut and paste the code for each component into its respective file.
4. Export the component from each file.
5. Import the components into the App.js file.
6. Update the App.js file to render the components.

**Code:**

```javascript
// App.js

import Logo from './components/Logo';
import Form from './components/Form';
import PackingList from './components/PackingList';
import Item from './components/Item';
import Stats from './components/Stats';

function App() {
  return (
    <div>
      <Logo />
      <Form />
      <PackingList />
      <Stats />
    </div>
  );
}

export default App;
```

```javascript
// Logo.js

export default function Logo() {
  return (
    <img src="/logo.png" alt="Logo" />
  );
}
```

```javascript
// Form.js

import { useState } from 'react';

export default function Form() {
  const [item, setItem] = useState('');

  function handleAddItem() {
    // Add the item to the packing list.
  }

  return (
    <form onSubmit={handleAddItem}>
      <input
        type="text"
        placeholder="Item"
        value={item}
        onChange={(e) => setItem(e.target.value)}
      />
      <button type="submit">Add item</button>
    </form>
  );
}
```

```javascript
// PackingList.js

import Item from './Item';

export default function PackingList() {
  const items = ['shorts', 'charger'];

  return (
    <ul>
      {items.map((item) => (
        <Item key={item}>{item}</Item>
      ))}
    </ul>
  );
}
```

```javascript
// Item.js

export default function Item({ item }) {
  return (
    <li>{item}</li>
  );
}
```

```javascript
// Stats.js

export default function Stats() {
  // Calculate the stats.
  return (
    <div>
      <p>Total items: {items.length}</p>
      <p>Total weight: {weight}</p>
    </div>
  );
}
```

**Once we have split the App.js file into multiple component files, we can move the component files to a new components folder. This will make our code more organized and easier to maintain.**

#  The "children" Prop: Making a Reusable Button

**Detailed notes with code on the children prop in React:**

**What is the children prop?**

The children prop is a special prop that is automatically passed to every React component. It is an array of all the JSX elements that are between the opening and closing tags of the component.

**How to use the children prop**

To use the children prop, you simply need to access it in your component's code. For example, the following code shows how to access the children prop in a button component:

```javascript
function Button({ children }) {
  return (
    <button>
      {children}
    </button>
  );
}
```

You can then use the children prop to render any JSX content that you want inside the component. For example, the following code shows how to use the children prop to render a span element with text and an emoji:

```javascript
<Button>
  <span>Previous 👈</span>
</Button>
```

**When to use the children prop**

The children prop is a very powerful tool that can be used to make your React components more reusable and flexible. It is a good idea to use the children prop whenever you want to allow your components to render any JSX content that the parent component passes in.

**Example of using the children prop**

The following example shows how to use the children prop to create a reusable button component that can be used to render any JSX content that the parent component passes in:

```javascript
function Button({ children }) {
  return (
    <button>
      {children}
    </button>
  );
}

// Usage:

<Button>
  <span>Previous 👈</span>
</Button>

<Button>
  <span>Next 👉</span>
</Button>
```

In this example, both of the buttons will render the same JSX content, but we could easily change the content of the buttons by passing in different JSX elements to the children prop.

**Conclusion**

The children prop is a very important part of React, and it is something that you should use often to make your components more reusable and flexible.

# More Reusability With the "children" Prop

### Detailed notes with code from the paragraph given:

**Creating a reusable StepMessage component:**

1. Create a new file called `StepMessage.js` and paste the following code into it:

```javascript
import React from 'react';

function StepMessage({ step, children }) {
  return (
    <div className="step-message">
      <h3>Step {step}</h3>
      {children}
    </div>
  );
}

export default StepMessage;
```

This component accepts two props: `step` and `children`. The `step` prop is the step number, and the `children` prop is the content of the message.

2. Import the `StepMessage` component into your app.js file and use it as follows:

```javascript
import React from 'react';
import StepMessage from './StepMessage';

function App() {
  const steps = [
    'Step 1',
    'Step 2',
    'Step 3',
  ];

  return (
    <div>
      {steps.map((step) => (
        <StepMessage key={step} step={step}>
          This is the content for step {step}.
        </StepMessage>
      ))}
    </div>
  );
}

export default App;
```

This will render a list of `StepMessage` components, each with the step number and the content for that step.

**Passing props to the `StepMessage` component:**

You can pass any props to the `StepMessage` component that you want, including strings, numbers, objects, and arrays. You can also pass in JSX elements.

For example, the following code shows how to pass a different background color and text color to the `StepMessage` component:

```javascript
import React from 'react';
import StepMessage from './StepMessage';

function App() {
  const steps = [
    {
      step: 1,
      backgroundColor: 'red',
      textColor: 'white',
    },
    {
      step: 2,
      backgroundColor: 'green',
      textColor: 'white',
    },
    {
      step: 3,
      backgroundColor: 'blue',
      textColor: 'white',
    },
  ];

  return (
    <div>
      {steps.map((step) => (
        <StepMessage
          key={step.step}
          step={step.step}
          backgroundColor={step.backgroundColor}
          textColor={step.textColor}
        >
          This is the content for step {step.step}.
        </StepMessage>
      ))}
    </div>
  );
}

export default App;
```

This will render a list of `StepMessage` components, each with a different background color and text color.

**Using the `children` prop:**

The `children` prop is a special prop that allows you to pass any JSX content to a component. This can be useful when you want to create a reusable component that can display different types of content.

For example, the following code shows how to pass a button element to the `StepMessage` component:

```javascript
import React from 'react';
import StepMessage from './StepMessage';

function App() {
  const steps = [
    {
      step: 1,
      content: <button>Learn more</button>,
    },
    {
      step: 2,
      content: <button>Take a quiz</button>,
    },
    {
      step: 3,
      content: <button>Download the code</button>,
    },
  ];

  return (
    <div>
      {steps.map((step) => (
        <StepMessage key={step.step} step={step.step}>
          {step.content}
        </StepMessage>
      ))}
    </div>
  );
}

export default App;
```

This will render a list of `StepMessage` components, each with a button element.

**Conclusion:**

The `children` prop is a very powerful tool that can be used to create reusable and flexible React components. It is a good idea to use the `children` prop whenever you want to allow your components to render any JSX content that the parent component passes in.

# 
