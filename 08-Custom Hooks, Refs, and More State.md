# React Hooks and Their Rules

### Detailed Notes with Code

**What are React Hooks?**

React Hooks are special functions that allow us to use state and other React features in function components. They were introduced in React 16.8 and have quickly become one of the most popular features of the library.

**Why are React Hooks useful?**

Before React Hooks, the only way to use state and other React features in function components was to write a class. This can be cumbersome and verbose, especially for simple components. React Hooks allow us to write more concise and readable code.

**What are the rules of React Hooks?**

There are two rules for using React Hooks:

1. **Hooks can only be called at the top level of a component.** This means that we cannot call Hooks inside conditions, loops, or nested functions.
2. **Hooks can only be called from React functions.** This means that Hooks cannot be called from regular JavaScript functions or class components.

**How do React Hooks work?**

React Hooks rely on a linked list of hooks that is associated with each component instance. This linked list is used to track the order in which Hooks were called.

**Why do Hooks need to be called in the same order on every render?**

Hooks need to be called in the same order on every render so that React can correctly associate each Hook with its value. This is because the order in which a Hook is called uniquely identifies the Hook.

**Example**

```javascript
// This code violates the first rule of hooks
function MyComponent() {
  if (true) {
    const [stateA, setStateA] = useState(23);
  }

  const [stateB, setStateB] = useState('');

  useEffect(() => {
    // ...
  }, [stateA]);

  return (
    <div>
      <h1>{stateA}</h1>
      <h1>{stateB}</h1>
    </div>
  );
}
```

This code will not work because the `useState` Hook is called conditionally. This means that the order in which the Hooks are called will change on every render, which will break the linked list of hooks.

**Conclusion**

React Hooks are a powerful way to use state and other React features in function components. They are easy to learn in the beginning, but it is important to understand the rules of Hooks in order to use them effectively.

# The Rules of Hooks in Practice

### Detailed Notes with Code

**Breaking the Rules of React Hooks**

**Overview**

This section of the video demonstrates how to break the rule of hooks that states that hooks can only be called at the top level of a component. This is done by conditionally calling a hook in the `MovieDetails` component.

**Code Example**

```javascript
// This code violates the first rule of hooks
function MovieDetails() {
  const imdbRating = 8.7;

  if (imdbRating > 8) {
    const [isTop, setIsTop] = useState(true);
  }

  return (
    <div>
      <h1>{imdbRating}</h1>
    </div>
  );
}
```

**Explanation**

When the `MovieDetails` component is rendered, React creates a linked list of hooks. This linked list contains a reference to each hook in the component, in the order in which they were called.

The rule of hooks that states that hooks can only be called at the top level of a component ensures that the linked list of hooks is always the same, regardless of the component's state.

If we conditionally call a hook, we are essentially changing the order in which the hooks are called. This will break the linked list of hooks, and React will not be able to correctly associate each hook with its value.

**Error Message**

When we try to render the `MovieDetails` component with the conditional hook, React throws the following error message:


React has detected a change in the order of hooks called in this component. This is not supported because it can lead to bugs and unexpected behavior. To fix this, make sure that all hooks are called in the same order on every render.


**Conclusion**

It is important to avoid conditionally calling hooks, as this can lead to bugs and unexpected behavior. If you need to conditionally use state or other React features, you should use a custom hook instead.

**Additional Considerations**

* ESLint can be used to warn us about the potential dangers of conditionally calling hooks.
* Early returns can also break the linked list of hooks, even if we are not explicitly calling hooks inside of the early return.
* It is important to understand the rules of hooks in order to use them effectively.

# More Details of useState

### Detailed Notes with Code

**useState Hook Important Details**

**Overview**

This section of the video reviews some important details about the `useState` hook, including:

* The initial value passed into `useState` is only used on the initial render.
* Updating state is asynchronous.
* We can use a callback function to access the updated state after it has been set.
* We can also use a callback function to initialize state.

**Code Example 1**

```javascript
// This code demonstrates that the initial value passed into useState is only used on the initial render.
const isTop = imdbRating > 8; // This will be false because the IMDB rating is undefined when the component first mounts.

// useState will only look at the initial value on the initial render.
const [isTopState, setIsTopState] = useState(isTop);

console.log(isTopState); // false
```

**Explanation**

The `useState` hook will only look at the initial value on the initial render. This is because the initial value is used to initialize the state. Once the state has been initialized, it can only be updated using the `useState` setter function.

**Code Example 2**

```javascript
// This code demonstrates that updating state is asynchronous.
const [avgRating, setAvgRating] = useState(0);

// setAvgRating is an asynchronous function.
setAvgRating(imdbRating);

console.log(avgRating); // 0
```

**Explanation**

Updating state is asynchronous because React uses a batching mechanism to update state. This means that React will not update the state immediately after it is called. Instead, React will wait until the end of the event loop to update the state. This allows React to improve performance by batching together multiple state updates.

**Code Example 3**

```javascript
// This code demonstrates how to use a callback function to access the updated state after it has been set.
const [avgRating, setAvgRating] = useState(0);

setAvgRating((currentAvgRating) => {
  return currentAvgRating + imdbRating;
});

console.log(avgRating); // 8.6
```

**Explanation**

We can use a callback function to access the updated state after it has been set by passing the callback function as the second argument to the `useState` setter function. React will then call the callback function with the current state value as the argument.

**Code Example 4**

```javascript
// This code demonstrates how to use a callback function to initialize state.
const [avgRating, setAvgRating] = useState(() => {
  return imdbRating;
});
```

**Explanation**

We can use a callback function to initialize state by passing the callback function as the first argument to the `useState` hook. React will then call the callback function to initialize the state.

**Conclusion**

It is important to understand the following important details about the `useState` hook:

* The initial value passed into `useState` is only used on the initial render.
* Updating state is asynchronous.
* We can use a callback function to access the updated state after it has been set.
* We can also use a callback function to initialize state.

# Initializing State With a Callback (Lazy Initial State)

### Detailed Notes with Code

**Persisting the Watch List in Local Storage**

**Overview**

In this lecture, we learn how to persist the watch list in local storage using the `useState` hook. We do this in two parts:

1. We store the watched movies in local storage each time they are updated.
2. We read the data back from local storage and store it in the watched state when the app component mounts.

**Code Example 1**

```javascript
// Store the watched movies in local storage each time they are updated.
useEffect(() => {
  const watched = JSON.stringify(watchedMovies);
  localStorage.setItem('watched', watched);
}, [watchedMovies]);
```

**Explanation**

This effect will run each time the `watchedMovies` state is updated. When the effect runs, it will convert the `watchedMovies` state to a string using `JSON.stringify()`. Then, it will store the string in local storage using `localStorage.setItem()`.

**Code Example 2**

```javascript
// Read the data back from local storage and store it in the watched state
// when the app component mounts.
const [watchedMovies, setWatchedMovies] = useState(() => {
  const watched = localStorage.getItem('watched');
  if (watched) {
    return JSON.parse(watched);
  } else {
    return [];
  }
});
```

**Explanation**

The `useState` hook accepts a callback function as the initial value of the state. This callback function is only executed once, when the component mounts.

In the callback function, we read the `watched` data from local storage using `localStorage.getItem()`. If the data exists, we convert it back to an array using `JSON.parse()`. Otherwise, we return an empty array.

**Conclusion**

By using the `useState` hook in this way, we can persist the watch list in local storage. This means that the watch list will be preserved even if the user reloads the page or closes the browser.

# useState Summary

**useState Hook Summary**

**Creating State**

* Simple way: Pass a single value as the initial value to `useState()`.
* Callback function way: Pass a callback function as the initial value to `useState()`. This callback function is only executed once, when the component mounts, and it should return the initial state value.

**Updating State**

* Simple way: Pass a single value as the next state to the `useState()` setter function.
* Callback function way: Pass a callback function to the `useState()` setter function. This callback function should be pure and should return the next state value based on the current state value.

**Important Rule**

Never mutate objects or arrays when updating state. Instead, create a new object or a new array which incorporates the changes that you want to make, and then pass that new object or array into the `useState()` setter function.

**Code Examples**

```javascript
// Simple way to create state
const [count, setCount] = useState(0);

// Callback function way to create state
const [watchedMovies, setWatchedMovies] = useState(() => {
  const watched = localStorage.getItem('watched');
  if (watched) {
    return JSON.parse(watched);
  } else {
    return [];
  }
});

// Simple way to update state
setCount(1000);

// Callback function way to update state
setCount((prevState) => prevState + 1);
```

# How NOT to Select DOM Elements in React

### Detailed Notes with Code

**Manually Selecting a DOM Element**

**Overview**

In this lecture, we learn how to manually select a DOM element using `useEffect`. However, we quickly see that this is not the React way of doing things. It is not declarative and it can lead to problems such as having to add classes or IDs just for the purpose of selecting, and re-selecting the element over and over again.

**Code Example**

```javascript
// Manually select a DOM element using useEffect
useEffect(() => {
  const el = document.querySelector('.search');
  el.focus();
}, []);
```

**Problems with Manually Selecting a DOM Element**

* It is not declarative.
* It can lead to problems such as having to add classes or IDs just for the purpose of selecting, and re-selecting the element over and over again.

**Solution: Refs**

Refs allow us to select DOM elements in a more declarative way. We will learn about refs in the next video.

**Conclusion**

Manually selecting a DOM element is not the React way of doing things. It is better to use refs to select DOM elements in a more declarative way.

# Introducing Another Hook: useRef

## Notes on the useRef hook in React

**What is a ref?**

A ref is a reference to a DOM element or React element. It is a mutable value that persists across renders. This means that you can use refs to store data that you need to access between renders, such as the focus state of an input field or the dimensions of a DOM element.

**How to use the useRef hook**

To use the useRef hook, you first need to import it from React:

```javascript
import React, { useRef } from "react";
```

Then, you can declare a ref using the useRef function:

```javascript
const ref = useRef();
```

This will create a ref object with a mutable current property. You can then assign a DOM element or React element to the current property using the ref attribute:

```javascript
<input ref={ref} />
```

**Use cases for refs**

There are two main use cases for refs:

* **To store data that needs to be persisted across renders.** For example, you can use a ref to store the focus state of an input field so that it can be restored when the component re-renders.
* **To access DOM elements or React elements directly.** For example, you can use a ref to get the dimensions of a DOM element or to focus an input field.

**Differences between state and refs**

State and refs are both ways to store data in React components, but they have some important differences:

* **State is immutable, but refs are not.** This means that when you update state, React creates a new copy of the state object. With refs, on the other hand, you are directly mutating the ref object.
* **Updating state causes a re-render, but updating refs does not.** This is because state is used to render the component, while refs are used to store data that is not used for rendering.
* **State updates are asynchronous, but ref updates are not.** This means that you cannot use the new state immediately after updating it. With refs, on the other hand, you can read the new current property immediately after updating it.

**When to use state and when to use refs**

You should use state to store data that needs to trigger a re-render when it changes. For example, you should use state to store the value of an input field or the selected item in a list.

You should use refs to store data that needs to be persisted across renders but does not need to trigger a re-render. For example, you should use a ref to store the focus state of an input field or the dimensions of a DOM element.

**Examples of using refs**

Here are some examples of how to use refs in React:

```javascript
// Focus an input field when the component mounts
const inputRef = useRef();

useEffect(() => {
  inputRef.current.focus();
}, []);

// Store the dimensions of a DOM element
const divRef = useRef();

useEffect(() => {
  const width = divRef.current.clientWidth;
  const height = divRef.current.clientHeight;

  // Do something with the width and height
}, []);

// Get the selected item in a list
const listRef = useRef();

const selectedItem = listRef.current.querySelector(".selected");

// Do something with the selected item
```

**Conclusion**

The useRef hook is a powerful tool that can be used to store data that needs to be persisted across renders or to access DOM elements or React elements directly.

# Refs to Select DOM Elements

## Notes on using refs to select DOM elements in React

**What is a ref?**

A ref is a reference to a DOM element or React element. It is a mutable value that persists across renders. This means that you can use refs to store data that you need to access between renders, such as the focus state of an input field or the dimensions of a DOM element.

**How to use the useRef hook to select DOM elements**

To use the useRef hook to select DOM elements, you first need to import it from React:

```javascript
import React, { useRef } from "react";
```

Then, you can declare a ref using the useRef function:

```javascript
const inputRef = useRef();
```

This will create a ref object with a mutable current property. You can then assign a DOM element to the current property using the ref prop:

```javascript
<input ref={inputRef} />
```

**When to use refs to select DOM elements**

You should use refs to select DOM elements when you need to access them directly or when you need to store data about them between renders. For example, you might use a ref to:

* Focus an input field when the component mounts
* Get the dimensions of a DOM element
* Get the selected item in a list
* Implement a feature like the one in the example, where you want to clear the search query when the user hits the Enter key

**Example**

The following code shows how to use a ref to select an input element and focus it when the component mounts:

```javascript
import React, { useRef } from "react";

const MyComponent = () => {
  const inputRef = useRef();

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return (
    <input ref={inputRef} />
  );
};
```

The following code shows how to use a ref to get the dimensions of a DOM element:

```javascript
import React, { useRef } from "react";

const MyComponent = () => {
  const divRef = useRef();

  const dimensions = () => {
    return {
      width: divRef.current.clientWidth,
      height: divRef.current.clientHeight,
    };
  };

  return (
    <div ref={divRef}>
      <p>The dimensions of this div are: {dimensions().width}px x {dimensions().height}px</p>
    </div>
  );
};
```

The following code shows how to use a ref to get the selected item in a list:

```javascript
import React, { useRef } from "react";

const MyComponent = () => {
  const listRef = useRef();

  const selectedItem = () => {
    return listRef.current.querySelector(".selected");
  };

  return (
    <ul ref={listRef}>
      <li>Item 1</li>
      <li className="selected">Item 2</li>
      <li>Item 3</li>
    </ul>
  );
};
```

**Conclusion**

Refs are a powerful tool that can be used to select DOM elements directly or to store data about them between renders. However, it is important to use them wisely, as they can lead to performance problems if used incorrectly.

# Refs to Persist Data Between Renders
## Notes on using refs to store data that needs to be persisted between renders

**What is a ref?**

A ref is a reference to a DOM element or React element. It is a mutable value that persists across renders. This means that you can use refs to store data that you need to access between renders, such as the focus state of an input field or the dimensions of a DOM element.

**When to use refs to store data that needs to be persisted between renders**

You should use refs to store data that needs to be persisted between renders but that does not need to trigger a re-render. For example, you might use a ref to store:

* The number of times the user clicks a button before submitting a form
* The ID of a timer so that you can stop it later
* The dimensions of a DOM element so that you can position it correctly

**Example**

The following code shows how to use a ref to store the number of times the user clicks a button before submitting a form:

```javascript
import React, { useRef } from "react";

const MyComponent = () => {
  const clickCountRef = useRef(0);

  const handleClick = () => {
    clickCountRef.current++;
  };

  const handleSubmit = () => {
    const clickCount = clickCountRef.current;

    // Do something with the click count
  };

  return (
    <div>
      <button onClick={handleClick}>Click Me</button>
      <button onClick={handleSubmit}>Submit</button>
    </div>
  );
};
```

The following code shows how to use a ref to store the ID of a timer so that you can stop it later:

```javascript
import React, { useRef } from "react";

const MyComponent = () => {
  const timerIdRef = useRef();

  const startTimer = () => {
    timerIdRef.current = setInterval(() => {
      // Do something
    }, 1000);
  };

  const stopTimer = () => {
    clearInterval(timerIdRef.current);
  };

  return (
    <div>
      <button onClick={startTimer}>Start Timer</button>
      <button onClick={stopTimer}>Stop Timer</button>
    </div>
  );
};
```

**Conclusion**

Refs are a powerful tool that can be used to store data that needs to be persisted between renders but that does not need to trigger a re-render. However, it is important to use them wisely, as they can lead to performance problems if used incorrectly.

# What are Custom Hooks? When to Create One?

## Notes on custom hooks

**What are custom hooks?**

Custom hooks are a way to reuse stateful logic between multiple components in React. They are functions that start with the word `use` and use one or more built-in React hooks.

**When to create a custom hook**

You should create a custom hook if you have a piece of logic that you want to reuse in multiple components and that contains one or more built-in React hooks.

**Benefits of using custom hooks**

There are several benefits to using custom hooks:

* **Reusability:** Custom hooks allow you to reuse logic between multiple components, which can make your code more efficient and maintainable.
* **Abstraction:** Custom hooks can be used to abstract away complex logic, making it easier to use and understand.
* **Portability:** Custom hooks can be shared and reused across different projects.

**Example**

The following code shows a simple custom hook for fetching data:

```javascript
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        const data = await response.json();
        setData(data);
        setIsLoading(false);
      } catch (error) {
        setError(error);
        setIsLoading(false);
      }
    }

    fetchData();
  }, [url]);

  return { data, isLoading, error };
};
```

This custom hook can be used in any component to fetch data from the given URL. The following code shows how to use the custom hook:

```javascript
import React, { useFetch } from "react";

const MyComponent = () => {
  const { data, isLoading, error } = useFetch("https://example.com/api/users");

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>Error: {error.message}</div>;
  }

  return <ul>{data.map((user) => <li key={user.id}>{user.name}</li>)}</ul>;
};
```

The `useFetch` custom hook takes care of fetching the data, loading state, and error handling. This makes the `MyComponent` component simpler and easier to read.

**Conclusion**

Custom hooks are a powerful tool for reusability, abstraction, and portability. If you have logic that you want to reuse in multiple components and that contains one or more built-in React hooks, you should consider creating a custom hook.

# Creating our First Custom Hook: useMovies

**Detailed notes on extracting a custom hook from a React component**

**Introduction**

A custom hook is a JavaScript function that uses one or more React hooks to encapsulate common logic that can be reused across multiple components.

**Steps**

To extract a custom hook from a React component, follow these steps:

1. **Identify the logic that you want to extract.** This should be a piece of logic that is self-contained, reusable, and non-visual.
2. **Create a new file for your custom hook.** This file should contain the following:
    * A function declaration with a name that starts with the word `use`.
    * Any necessary imports.
    * The logic that you want to extract from your component.
    * A return statement that returns the values that you want to make available to the components that use your custom hook.
3. **Update your component to use the custom hook.** Import the custom hook into your component and call it like any other function. Pass in any necessary arguments and destructure the returned values into your component's state.

**Example**

The following example shows how to extract a custom hook to fetch movies from an API:

```javascript
// useMovies.js

import { useState, useEffect } from "react";

const useMovies = (query) => {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchMovies() {
      try {
        const response = await fetch(`https://api.themoviedb.org/3/search/movie?query=${query}&api_key=YOUR_API_KEY`);
        const data = await response.json();
        setMovies(data.results);
        setIsLoading(false);
      } catch (error) {
        setError(error);
        setIsLoading(false);
      }
    }

    fetchMovies();
  }, [query]);

  return { movies, isLoading, error };
};
```

```javascript
// App.js

import React, { useMovies } from "react";

const App = () => {
  const { movies, isLoading, error } = useMovies("star wars");

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>Error: {error.message}</div>;
  }

  return <ul>{movies.map((movie) => <li key={movie.id}>{movie.title}</li>)}</ul>;
};
```

**Benefits**

Extracting custom hooks from React components has several benefits:

* **Reusability:** Custom hooks can be reused across multiple components, which can reduce code duplication and improve maintainability.
* **Abstraction:** Custom hooks can abstract away complex logic, making it easier to use and understand.
* **Portability:** Custom hooks can be shared and reused across different projects.

**Conclusion**

Custom hooks are a powerful tool for promoting reusability, abstraction, and portability in React applications. If you have a piece of logic that is self-contained, reusable, and non-visual, consider extracting it into a custom hook.

# Creating useLocalStorageState

## Detailed notes on creating a custom hook to store state in local storage

**Introduction**

A custom hook is a JavaScript function that uses one or more React hooks to encapsulate common logic that can be reused across multiple components.

In this lecture, we will create a custom hook to store state in local storage. This will allow us to easily persist state across renders and page reloads.

**Steps**

To create a custom hook to store state in local storage, follow these steps:

1. Create a new file for your custom hook. This file should contain the following:
    * A function declaration with a name that starts with the word `use`.
    * Any necessary imports.
    * The logic to read and write state from local storage.
    * A return statement that returns the state variable and the state setter function.

2. Import your custom hook into the components that need to use it.
3. Call your custom hook and pass in the initial state value.
4. Destructure the returned state variable and state setter function into your component's state.

**Example**

The following code shows an example of a custom hook to store state in local storage:

```javascript
// useLocalStorageState.js

import { useState, useEffect } from "react";

const useLocalStorageState = (key, initialState) => {
  const [state, setState] = useState(() => {
    const storedValue = localStorage.getItem(key);
    return storedValue ? JSON.parse(storedValue) : initialState;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(state));
  }, [state, key]);

  return [state, setState];
};
```

This custom hook works by first checking if the state value is already stored in local storage. If it is, the value is read from local storage and returned as the initial state. Otherwise, the initial state value that is passed in is used.

Every time the state value changes, the custom hook updates the value in local storage.

**Usage**

The following code shows how to use the `useLocalStorageState` custom hook:

```javascript
// App.js

import React, { useLocalStorageState } from "react";

const App = () => {
  const [watched, setWatched] = useLocalStorageState("watched", []);

  return (
    <ul>
      {watched.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
};
```

This component uses the `useLocalStorageState` custom hook to store the `watched` state value in local storage. This means that the `watched` state value will be persisted across renders and page reloads.

**Benefits**

Using custom hooks to store state in local storage has several benefits:

* Reusability: Custom hooks can be reused across multiple components, which can reduce code duplication and improve maintainability.
* Abstraction: Custom hooks can abstract away the complexity of managing local storage, making it easier to use and understand.
* Portability: Custom hooks can be shared and reused across different projects.

**Conclusion**

Custom hooks are a powerful tool for promoting reusability, abstraction, and portability in React applications. If you need to store state in local storage, consider using a custom hook to do so.

# Creating useKey

## Detailed notes on creating a custom hook to handle key presses

### Introduction

A custom hook is a JavaScript function that uses one or more React hooks to encapsulate common logic that can be reused across multiple components.

In this lecture, we will create a custom hook to handle key presses. This will allow us to easily listen for and respond to key presses in our components.

### Steps

To create a custom hook to handle key presses, follow these steps:

1. Create a new file for your custom hook. This file should contain the following:
    * A function declaration with a name that starts with the word `use`.
    * Any necessary imports.
    * The logic to listen for and respond to key presses.
    * A return statement that returns a function that can be used to listen for and respond to key presses.

2. Import your custom hook into the components that need to use it.
3. Call your custom hook and pass in the callback function that should be executed when the specified key is pressed.
4. Use the returned function to listen for key presses.

### Example

The following code shows an example of a custom hook to handle key presses:

```javascript
// useKey.js

import { useEffect } from "react";

const useKey = (key, callback) => {
  useEffect(() => {
    const handleKeyPress = (event) => {
      if (event.key === key) {
        callback(event);
      }
    };

    window.addEventListener("keydown", handleKeyPress);

    return () => {
      window.removeEventListener("keydown", handleKeyPress);
    };
  }, [key, callback]);
};
```

This custom hook works by listening for key down events on the window object. When a key down event is detected, the custom hook checks if the pressed key is the specified key. If it is, the callback function is executed.

### Usage

The following code shows how to use the `useKey` custom hook:

```javascript
// App.js

import React, { useKey } from "react";

const App = () => {
  const onCloseMovie = () => {
    // Close the movie
  };

  useKey("Escape", onCloseMovie);

  return (
    <div>
      <h1>Movie App</h1>
      <button onClick={onCloseMovie}>Close Movie</button>
    </div>
  );
};
```

This component uses the `useKey` custom hook to listen for the escape key to be pressed. When the escape key is pressed, the `onCloseMovie` callback function is executed.

### Benefits

Using custom hooks to handle key presses has several benefits:

* Reusability: Custom hooks can be reused across multiple components, which can reduce code duplication and improve maintainability.
* Abstraction: Custom hooks can abstract away the complexity of handling key presses, making it easier to use and understand.
* Portability: Custom hooks can be shared and reused across different projects.

### Conclusion

Custom hooks are a powerful tool for promoting reusability, abstraction, and portability in React applications. If you need to handle key presses in your components, consider using a custom hook to do so.



