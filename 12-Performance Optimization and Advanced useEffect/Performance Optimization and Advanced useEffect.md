# Performance Optimization and Wasted Renders

Sure, here are detailed notes with code from the paragraph you provided:

**Overview of React Optimization**

Optimizing React applications involves three main areas: preventing wasted renders, improving overall app speed and responsiveness, and reducing bundle size.

**Preventing Wasted Renders**

1. **Memoize Components with `memo`:** Wrap components with React's `memo` function to prevent unnecessary re-renders.

```javascript
import React from 'react';
import memo from 'react-memo';

const MyComponent = ({ prop }) => {
  // ... component logic
  return <div>{prop}</div>;
};

const MyMemoizedComponent = memo(MyComponent);
```

2. **Memorize Objects and Functions with `useMemo` and `useCallback`:** Use React's `useMemo` and `useCallback` hooks to memoize expensive objects and functions, preventing unnecessary re-renders.

```javascript
import React, { useState, useMemo, useCallback } from 'react';

const MyComponent = () => {
  const [data, setData] = useState([]);

  const memoizedData = useMemo(() => {
    // Expensive data processing here
    return data;
  }, [data]);

  const memoizedCallback = useCallback(() => {
    // Expensive function here
  }, []);

  return (
    <div>
      {memoizedData.map((item) => <div key={item.id}>{item}</div>)}
      <button onClick={memoizedCallback}>Perform Expensive Operation</button>
    </div>
  );
};
```

3. **Pass Elements as Children or Props:** Pass children elements directly as props to prevent unnecessary re-renders.

```javascript
import React from 'react';

const MyComponent = ({ children }) => {
  return <div>{children}</div>;
};

const MyApp = () => (
  <MyComponent>
    <div>Child 1</div>
    <div>Child 2</div>
  </MyComponent>
);
```

**Improving Perceived App Speed**

1. **Use `useMemo` and `useCallback` Hooks:** Leverage `useMemo` and `useCallback` to optimize performance-critical computations.

2. **Use `useTransition` Hook:** Utilize the `useTransition` hook to delay rendering non-critical updates for smoother animations and transitions.

**Reducing Bundle Size**

1. **Minimize Third-party Packages:** Use fewer third-party packages to reduce the overall bundle size.

2. **Implement Code Splitting and Lazy Loading:** Employ code splitting and lazy loading techniques to load only the necessary code on demand, improving page loading performance.

**Understanding Wasted Renders**

A wasted render occurs when a component re-renders but doesn't cause any changes to the DOM (Document Object Model), resulting in unnecessary calculations and potential performance issues.

**Component Re-rendering Triggers**

1. **State Changes:** When a component's state changes, it triggers a re-render to reflect the updated state.

2. **Context Changes:** If a component is subscribed to a context, re-rendering occurs when the context value changes.

3. **Parent Component Re-rendering:** When a parent component re-renders, its child components are also re-rendered, even if their props haven't changed.

**Avoiding Wasted Renders**

1. **Optimize Component Structure:** Avoid nested components to minimize re-renders caused by parent component updates.

2. **Minimize State Updates:** Update state only when necessary, using techniques like `setState` batching or `useReducer` for complex state management.

3. **Memoize Components and Calculations:** Leverage `memo`, `useMemo`, and `useCallback` to prevent unnecessary re-renders and computations.

**Conclusion**

Optimizing React applications involves identifying and preventing wasted renders, improving overall app speed, and reducing bundle size to enhance user experience and performance.

# The Profiler Developer Tool

Sure, here are detailed notes with code from the paragraph given below:

**Analyzing Renders and Re-renders with React Profiler**

The React Developer Tools Profiler is a powerful tool for analyzing how components render and re-render in your React applications. It can help you identify performance bottlenecks and optimize your code for better performance.

**Recording a Profile**

To record a profile, click the record button in the Profiler tab. Then, interact with your application as you normally would. The Profiler will record information about each component that renders, including its name, how long it took to render, and the reason it re-rendered.

**Viewing the Profile Data**

Once you have finished recording, you can view the profile data in two different ways:

* **Flamegraph:** The flamegraph is a visual representation of the component hierarchy. The more yellow a component is, the longer it took to render.
* **Ranked Table:** The ranked table shows a list of all the components that rendered, sorted by how long they took to render.

**Understanding Why Components Re-render**

The Profiler also shows you the reason why each component re-rendered. The three possible reasons are:

* **State Update:** The component's own state was updated.
* **Context Update:** A context value that the component consumes was updated.
* **Parent Re-render:** The component's parent component re-rendered, causing all of its children to re-render.

**Using the Profiler to Identify Performance Bottlenecks**

The Profiler can be used to identify performance bottlenecks in your React applications. For example, you can use it to see which components are taking the longest to render and then investigate why those components are re-rendering so often.

**Playing Around with the Profiler**

I encourage you to experiment with the Profiler to get a better understanding of how it works. Try recording profiles of different interactions in your application and see how the data changes.

**Moving On**

In the next lecture, we will discuss our first small optimization trick.

# A Surprising Optimization Trick With children

Sure, here are detailed notes with code from the paragraph given below:

**Preventing Re-rendering with Children Prop**

This lecture introduces a simple performance optimization technique that utilizes the children prop to prevent certain components from re-rendering unnecessarily. This technique is not widely used but offers valuable insights into React's internal workings.

**The Problem: Unnecessary Re-rendering**

Consider a scenario where a "SlowComponent" is nested within a "Counter" component. The SlowComponent is computationally expensive, rendering a large array of 100,000 elements. Upon clicking a button in the Counter, the Counter's state updates, causing both the Counter and the SlowComponent to re-render.

**The Solution: Using Children Prop**

To prevent the SlowComponent from re-rendering unnecessarily, we can pass it as a prop to the Counter component instead of nesting it directly. This allows React to create the SlowComponent instance before the Counter component re-renders, making the SlowComponent unaffected by the Counter's state change.

**Understanding the Behavior**

When React encounters a JSX element with a children prop, it creates the corresponding component instance before rendering the parent component. In this case, the SlowComponent is created before the Counter re-renders, making it immune to the Counter's state change.

**Re-rendering Behavior with Context**

Similar to the children prop, components passed into a context provider are also created before the provider re-renders. This prevents unnecessary re-rendering of child components that don't consume the context.

**Real-world Applications**

This optimization technique can be useful in situations where a computationally expensive component is nested within a parent component that updates its state frequently. By passing the expensive component as a prop, we can prevent unnecessary re-renders and improve performance.

**Conclusion**

While this optimization technique may not be used all the time, understanding it provides deeper insights into React's internal workings and enhances your React development skills.

# Understanding memo

Sure, here are detailed notes with code from the paragraph given below:

**Memoization in React: Optimizing Component Re-renders**

**What is Memoization?**

Memoization is an optimization technique that aims to improve performance by caching the results of pure functions. In the context of React, we can utilize memoization to prevent unnecessary re-renders of components, thereby enhancing application performance.

**Introducing the memo Function**

React provides the `memo` function, which enables us to create memoized components. These components will not re-render if their props remain unchanged between renders. Essentially, memoization ensures that the component only re-renders when its input data (props) changes.

**Why Use Memoization?**

Memoizing components is particularly beneficial when dealing with performance-intensive components. These are components that render slowly or generate a significant amount of UI content, making their re-renders computationally expensive. By memoizing such components, we can minimize unnecessary re-renders and improve overall application responsiveness.

**When to Use Memoization**

Memoization is not a one-size-fits-all solution. It is most effective when applied to components that meet the following criteria:

* **Heavy components:** The component should be computationally expensive, causing a noticeable lag or delay during rendering.

* **Frequently rendered components:** The component should re-render frequently within the application.

* **Same props between renders:** The component's props should remain unchanged between consecutive renders.

**Limitations of Memoization**

Memoization only considers props as input data. If a component's own state changes or if there is a change in a context it consumes, the component will re-render regardless of memoization.

**Overuse of Memoization**

Excessive use of memoization can be counterproductive. It is important to identify components that genuinely benefit from memoization and avoid applying it indiscriminately.

**Conclusion**

Memoization is a valuable tool for optimizing React applications, particularly for performance-critical components. By understanding its principles and applying it judiciously, developers can enhance the performance and responsiveness of their React applications.

# memo in Practice

Sure, here are the detailed notes with code from the paragraph given:

**Memorizing a Component in React**

**Problem**

In React, components often re-render when their parent components re-render, even if their props have not changed. This can cause performance problems, especially for components that are expensive to render.

**Solution**

React provides a higher-order component called `memo` that can be used to memoize a component. This means that the component will only re-render if its props have changed.

**Example**

The following example shows how to memoize a component called `Archive`.

```javascript
import React from 'react';
import { memo } from 'react';

const Archive = ({ show }) => {
  // Create an array of 10,000 posts
  const posts = new Array(10000).fill({
    id: Math.random(),
    title: 'Lorem ipsum dolor sit amet',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam velit ipsum, eu aliquam enim. Donec velit lectus, a iaculis velit.',
  });

  return (
    <div>
      {show && (
        <ul>
          {posts.map((post) => (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.content}</p>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

const memoizedArchive = memo(Archive);
```

The `memoizedArchive` component will only re-render if the `show` prop changes.

**Using Objects as Props**

If you pass an object as a prop to a memoized component, the component will re-render even if the object reference has not changed. This is because React does a shallow comparison of props, which means that it only checks for equality of object references.

**Solution**

To fix this problem, you can use a custom equality function with the `memo` HOC. The following example shows how to do this:

```javascript
import React from 'react';
import { memo } from 'react';

const Archive = ({ show, archiveOptions }) => {
  // Create an array of 10,000 posts
  const posts = new Array(10000).fill({
    id: Math.random(),
    title: 'Lorem ipsum dolor sit amet',
    content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam velit ipsum, eu aliquam enim. Donec velit lectus, a iaculis velit.',
  });

  return (
    <div>
      {show && (
        <ul>
          {posts.map((post) => (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.content}</p>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

const archiveOptions = {
  show: false,
  title: 'Post Archive',
};

const memoizedArchive = memo(Archive, (prevProps, nextProps) => {
  return (
    prevProps.show === nextProps.show &&
    prevProps.archiveOptions.show === nextProps.archiveOptions.show &&
    prevProps.archiveOptions.title === nextProps.archiveOptions.title
  );
});
```

The `memo` HOC will now only re-render the `Archive` component if the `show` prop or the `archiveOptions` prop changes.

**Conclusion**

Memorizing a component can be a great way to improve performance, especially for components that are expensive to render. However, it is important to be aware of the limitations of memoization, such as the fact that it does not work with objects as props.

# Understanding useMemo and useCallback

Sure, here are the detailed notes with code from the paragraph given below:

**Memorizing Values with useMemo and useCallback**

**Problem**

In the previous lecture, we saw that the `memo` HOC does not work as expected when passing objects or functions as props to a child component. This is because React considers these props to be new on each render, even if they are the same objects or functions as before.

**Solution**

React provides two hooks, `useMemo` and `useCallback`, that can be used to memorize values and functions, respectively. These hooks can be used to preserve values and functions across renders, even if the objects or functions themselves are the same.

**How it Works**

Both `useMemo` and `useCallback` take a function and a dependency array as arguments. The function is used to generate the value or function to be memoized, and the dependency array is used to specify which values or functions the memoized value or function depends on.

If any of the dependencies in the dependency array change, the memoized value or function will be recalculated and a new reference will be returned. Otherwise, the cached value or function will be returned.

**Use Cases**

There are three main use cases for `useMemo` and `useCallback`:

1. **Making objects or functions stable for use with the `memo` HOC**
2. **Avoiding expensive recalculations on every render**
3. **Memorizing values that are used in the dependency array of other hooks**

**When to Use and When Not to Use**

It is important to use `useMemo` and `useCallback` judiciously. Overusing these hooks can lead to performance problems. In general, you should only use these hooks if one of the three use cases applies.

**Code Examples**

Here are some examples of how to use `useMemo` and `useCallback`:

```javascript
// Example of using useMemo to memorize an expensive calculation
const memoizedExpensiveCalculation = useMemo(() => {
  // Perform expensive calculation here
  return result;
}, [dependencies]);

// Example of using useCallback to memorize a function
const memoizedFunction = useCallback(() => {
  // Perform some action here
}, [dependencies]);

// Example of using useMemo to memorize an object
const memoizedObject = useMemo(() => {
  return {
    prop1: 'value1',
    prop2: 'value2',
  };
}, [dependencies]);
```

**Conclusion**

`useMemo` and `useCallback` are powerful tools for optimizing React components. By memorizing values and functions, you can improve the performance of your components and avoid unnecessary re-renders.

# useMemo in Practice

Sure, here are the detailed notes with code from the paragraph given below:

**Fixing the Archive Component with useMemo**

**Problem**

In the previous lecture, we created a memoized archive component that rendered a list of posts. However, the component was not performing as expected. This is because we were passing an object as a prop to the component, and objects are considered to be new on each render, even if they are the same object as before.

**Solution**

To fix this problem, we can use the `useMemo` hook to memorize the object. This will ensure that the object is only created once, on the initial render, and then reused on subsequent renders.

**Code**

Here is the code for the memoized archive component:

```javascript
import React from 'react';
import { useMemo } from 'react';

const Archive = ({ show, posts }) => {
  // Create an array of posts
  const filteredPosts = posts.filter((post) => post.title.includes('Lorem'));

  // Memoize the archiveOptions object
  const archiveOptions = useMemo(() => {
    return {
      show: show,
      title: `Post Archive (${filteredPosts.length})`,
    };
  }, [show, filteredPosts.length]);

  return (
    <div>
      {show && (
        <ul>
          {filteredPosts.map((post) => (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.content}</p>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

const memoizedArchive = memo(Archive);
```

In this code, we are using the `useMemo` hook to memorize the `archiveOptions` object. The first argument to `useMemo` is a callback function that returns the object to be memoized. The second argument to `useMemo` is a dependency array. If any of the values in the dependency array change, the memoized object will be recalculated.

In this case, the dependency array includes the `show` prop and the `filteredPosts.length` value. This means that the memoized object will only be recalculated if either the `show` prop changes or the number of filtered posts changes.

With this fix in place, the archive component will only re-render when the `show` prop changes or the number of filtered posts changes. This will improve the performance of the application.

**Conclusion**

The `useMemo` hook is a powerful tool for optimizing React components. By memorizing values, you can improve the performance of your components and avoid unnecessary re-renders.

# useCallback in Practice

Sure, here are the detailed notes with code from the paragraph given below:

**Optimizing the Archive Component with useCallback**

**Problem**

In the previous lecture, we fixed the issue of the archive component re-rendering unnecessarily by memorizing the object prop using `useMemo`. However, we are still facing a similar issue with the `handleAddPost` function prop. This function is being recreated on every render, causing the archive component to re-render as well.

**Solution**

To fix this issue, we can memorize the `handleAddPost` function prop using the `useCallback` hook. The `useCallback` hook is similar to `useMemo`, but it is specifically designed for memorizing functions.

**Code**

Here is the code for the memoized archive component with the `handleAddPost` function prop:

```javascript
import React from 'react';
import { useMemo, useCallback } from 'react';

const Archive = ({ show, posts, handleAddPost }) => {
  // Create an array of filtered posts
  const filteredPosts = posts.filter((post) => post.title.includes('Lorem'));

  // Memoize the archiveOptions object
  const archiveOptions = useMemo(() => {
    return {
      show: show,
      title: `Post Archive (${filteredPosts.length})`,
    };
  }, [show, filteredPosts.length]);

  // Memoize the handleAddPost function
  const memoizedHandleAddPost = useCallback(() => {
    handleAddPost();
  }, []);

  return (
    <div>
      {show && (
        <ul>
          {filteredPosts.map((post) => (
            <li key={post.id}>
              <h2>{post.title}</h2>
              <p>{post.content}</p>
            </li>
          ))}
        </ul>
      )}
      <button onClick={memoizedHandleAddPost}>Add Post</button>
    </div>
  );
};

const memoizedArchive = memo(Archive);
```

In this code, we are using the `useCallback` hook to memorize the `handleAddPost` function. The first argument to `useCallback` is a callback function that returns the function to be memoized. The second argument to `useCallback` is a dependency array. If any of the values in the dependency array change, the memoized function will be recalculated.

In this case, the dependency array is empty, which means that the memoized function will only be recalculated once, on the initial render. This ensures that the `handleAddPost` function is not recreated on every render, preventing the archive component from re-rendering unnecessarily.

**Conclusion**

The `useCallback` hook is a powerful tool for optimizing React components that receive function props. By memorizing functions, you can improve the performance of your components and avoid unnecessary re-renders.

# Optimizing Context Re-Renders

Sure, here are some detailed notes with code from the paragraph you provided:

## Preventing Wasted Renders Related to the Context API

### Guidelines

* **Memoize direct children of the context provider:** This prevents these components from re-rendering when the state in the context changes.

* **Memoize the object that is passed into the context:** This prevents the context from being recreated when the object changes, which can cause unnecessary re-renders.

* **Create a separate context for each state:** This prevents components from re-rendering when a state that they are not using changes.

### Examples

* **Memoizing direct children:**

```javascript
import React from 'react';
import { memo } from 'react';

const PostContextProvider = React.createContext();

const PostList = memo(() => {
  // Render the list of posts
});

const App = () => {
  return (
    <PostContextProvider.Provider value={{ posts: [] }}>
      <PostList />
    </PostContextProvider.Provider>
  );
};
```

* **Memoizing the object:**

```javascript
import React from 'react';
import { memo } from 'react';

const PostContextProvider = React.createContext();

const value = memo(() => ({
  posts: [],
  searchQuery: '',
}));

const PostList = () => {
  const { posts, searchQuery } = useContext(PostContextProvider);
  // Render the list of posts filtered by the search query
};

const App = () => {
  return (
    <PostContextProvider.Provider value={value}>
      <PostList />
    </PostContextProvider.Provider>
  );
};
```

* **Creating a separate context for each state:**

```javascript
import React from 'react';
import { createContext } from 'react';

const PostContext = createContext({ posts: [] });
const SearchQueryContext = createContext('');

const PostList = () => {
  const { posts } = useContext(PostContext);
  const { searchQuery } = useContext(SearchQueryContext);
  // Render the list of posts filtered by the search query
};

const App = () => {
  return (
    <PostContext.Provider value={{ posts: [] }}>
      <SearchQueryContext.Provider value={''}>
        <PostList />
      </SearchQueryContext.Provider>
    </PostContext.Provider>
  );
};
```

### Additional Notes

* It is only necessary to optimize your context if all of the following are true:
    * The state in the context needs to change all the time.
    * The context has many consumers.
    * The app is actually slow and laggy.

* The actual optimization of your context can be quite confusing because it will depend a lot on how you build your application and how you set up your context, and also, what exactly you pass into the context.

* Memorizing the direct children of the context provider is a good first step, but it may not be enough if the context has many consumers.

* Memoizing the object that is passed into the context can further reduce re-renders, but it is important to be careful not to memoize anything that is not actually needed.

* Creating a separate context for each state is the most effective way to prevent wasted renders, but it can also be the most complex.

I hope these notes are helpful!

# Optimizing Bundle Size With Code Splitting

Sure, here are some detailed notes with code from the paragraph you provided:

**Optimizing Bundle Size with Code Splitting and Lazy Loading**

### Overview

Code splitting is a technique for optimizing the performance of React applications by breaking the bundle into smaller chunks. This allows the browser to load only the code that is needed for the current page, rather than the entire application at once. Lazy loading is a technique for loading code on demand, which means that the code for a particular component is not loaded until it is actually needed. This can further improve performance by reducing the amount of code that needs to be loaded initially.

### Code Splitting with React's `lazy` Function

React provides a built-in `lazy` function for code splitting. The `lazy` function takes a function as an argument, which should call the dynamic import function to load the module containing the component. The lazy component should then be rendered inside a Suspense component, which allows us to show a fallback component while the lazy component is being loaded.

### Example of Code Splitting with Lazy Loading

```javascript
import React, { Suspense } from 'react';
import { lazy } from 'react';

const Homepage = lazy(() => import('./pages/Homepage'));
const Product = lazy(() => import('./pages/Product'));
const Pricing = lazy(() => import('./pages/Pricing'));
const Login = lazy(() => import('./pages/Login'));
const AppLayout = lazy(() => import('./pages/AppLayout'));
const PageNotFound = lazy(() => import('./pages/PageNotFound'));

const App = () => {
  return (
    <Suspense fallback={<SpinnerFullPage />}>
      <Routes>
        <Route path="/" element={<Homepage />} />
        <Route path="/product" element={<Product />} />
        <Route path="/pricing" element={<Pricing />} />
        <Route path="/login" element={<Login />} />
        <Route path="*" element={<PageNotFound />} />
      </Routes>
    </Suspense>
  );
};
```

### Benefits of Code Splitting and Lazy Loading

* Reduced initial load time
* Improved perceived performance
* More efficient resource usage
* Easier maintenance of the codebase

### Conclusion

Code splitting and lazy loading are essential techniques for optimizing the performance of React applications. By using these techniques, you can ensure that your users have a smooth and responsive experience.

# Don't Optimize Prematurely!

Sure, here are detailed notes with code from the paragraph you provided:

**Performance Optimization Dos and Don'ts**

**Dos**

* **Profile your application to identify performance bottlenecks.**
* **Memoize expensive re-renders or expensive calculations.**
* **Memoize the context value if the context has a lot of consumers and the state updates all the time.**
* **Memoize all the direct child components of the context provider.**
* **Set up two separate contexts: one for the actual state value and one for updating the state.**
* **Always implement code splitting and lazy loading for all the routes in your single page applications.**

**Don'ts**

* **Optimize prematurely.**
* **Wrap all your components into a `memo` or all your values and callbacks into `useMemo` and `useCallback`.**
* **Optimize context if it's not slow and if it doesn't have many consumers.**
* **Make your code unreadable and super messy by wrapping everything into a `useCallback` or a `useMemo`.**

**Additional Notes**

* **Use the profiler tool to identify performance bottlenecks.**
* **Focus on fixing real performance issues.**
* **Consider memoization, context optimization, and code splitting/lazy loading when optimizing your React application.**

**Code Examples**

```javascript
// Memoize an expensive calculation
const memoizedCalculation = useMemo(() => {
  // Perform the expensive calculation
}, [dependencies]);

// Memoize a context value
const memoizedContextValue = useMemo(() => {
  // Get the context value
  const contextValue = useContext(MyContext);

  // Process the context value
  const processedValue = someProcessing(contextValue);

  return processedValue;
}, [contextValue]);

// Memoize all direct child components of the context provider
const memoizedChildComponents = useMemo(() => {
  // Get the child components
  const childComponents = useChildren(MyContextProvider);

  // Memoize each child component
  const memoizedChildren = childComponents.map(childComponent => memo(childComponent));

  return memoizedChildren;
}, [childComponents]);

// Set up two separate contexts: one for the actual state value and one for updating the state
const StateContext = createContext({ value: 0 });
const UpdateContext = createContext(updater => updater({ value: 0 }));

// Update the state value using the update context
const MyComponent = () => {
  const { value } = useContext(StateContext);
  const updateState = useContext(UpdateContext);

  return (
    <div>
      <p>State value: {value}</p>
      <button onClick={() => updateState(state => ({ ...state, value: state.value + 1 }))}>Update state</button>
    </div>
  );
};

// Implement code splitting and lazy loading for all the routes in your single page application
const App = () => {
  return (
    <Suspense fallback={<SpinnerFullPage />}>
      <Routes>
        <Route path="/" element={lazy(() => import('./pages/Homepage'))} />
        <Route path="/product" element={lazy(() => import('./pages/Product'))} />
        <Route path="/pricing" element={lazy(() => import('./pages/Pricing'))} />
        <Route path="/login" element={lazy(() => import('./pages/Login'))} />
        <Route path="*" element={lazy(() => import('./pages/PageNotFound'))} />
      </Routes>
    </Suspense>
  );
};
```

I hope these notes are helpful!

# useEffect Rules and Best Practices

Sure, here are detailed notes with code from the paragraph you provided:

**useEffect Hook Dependency Array Rules and Guidelines**

**Rule 1: Include all reactive values in the dependency array**

* Reactive values include state, props, context values, and any other value that references one of the reactive values.
* The goal is to avoid stale closures.
* This rule is strict and tells us exactly what must be included in the dependency array.
* The dependencies choose themselves.
* Never ignore the ESLint rule warning about missing dependencies.

**Rule 2: Do not use objects or arrays as dependencies**

* Objects and arrays have different references each time they are recreated.
* React checks if dependencies have changed between renders using the triple equality operator.
* Even if the content of an object stays the same, React will see the old and new object as different and will rerun the effect.

**Rule 3: Use useCallback for helper functions as dependencies**

* If you can't move the function inside the effect, memoize it with useCallback.
* If the function is not a reactive value itself, move it entirely out of the component.

**Rule 4: Use only primitive values from objects as dependencies**

* If you need to use an object as a dependency, only include the properties that you actually need inside the effect.
* This only works if the properties are primitive values.

**Rule 5: Use useReducer for multiple related reactive values**

* A reducer can be a secret weapon to make dependency problems go away.

**Rule 6: Do not include setState or dispatch in the dependency array**

* React guarantees that these functions are stable between renders.

**Rule 7: Use effects as a last resort**

* Effects are an escape hatch to step outside of React.

**Common useEffect Overuse Cases**

* Responding to user events
* Fetching data from an API on mount
* Synchronizing state changes

**Alternatives to useEffect**

* Event handlers for user events
* Data fetching libraries like React Query
* Derived state and event handlers for state synchronization

**General Advice**

* Everything is acceptable in certain situations and in certain doses.
* Rely on derived state and event handlers instead of using effects to set state based on another state.

# Setting State Based on Other State Updates

Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Implement functionality to adjust the duration manually using buttons.

**Problem:**

Currently, the duration is derived from four state variables and is updated only when one of these variables changes. This makes it difficult to manually adjust the duration using buttons.

**Solution:**

1. **Make duration a state variable:** Replace the derived duration with a state variable `duration` using `useState`.

```javascript
const [duration, setDuration] = useState(0);
```
2. **Update duration using useEffect:** Implement a `useEffect` hook to update the `duration` state variable whenever any of the four state variables (number, sets, speed, duration of break) change.

```javascript
useEffect(() => {
  setDuration(calculateDuration());
}, [number, sets, speed, breakDuration]);
```
3. **Implement button event handlers:** Create separate event handlers `handleInc` and `handleDec` to increment and decrement the duration, respectively.

```javascript
function handleInc() {
  const currentDuration = getDuration();
  const newDuration = Math.floor(currentDuration) + 1;
  setDuration(newDuration);
}

function handleDec() {
  const currentDuration = getDuration();
  const newDuration = Math.max(Math.floor(currentDuration) - 1, 0);
  setDuration(newDuration);
}
```

4. **Attach button event handlers:** Connect the `handleInc` and `handleDec` functions to the respective buttons.

```javascript
<button onClick={handleInc}>Increase</button>
<button onClick={handleDec}>Decrease</button>
```

**Considerations:**

- Using `useEffect` to update state based on another state update is not always desirable.
- This approach can result in multiple renders due to the asynchronous nature of `useEffect`.
- Consider avoiding this approach when possible, especially when handling performance-critical components.

**Code:**

```javascript
import React, { useState, useEffect } from 'react';

const calculateDuration = () => {
  // Calculate duration based on number, sets, speed, breakDuration
};

function App() {
  const [number, setNumber] = useState(1);
  const [sets, setSets] = useState(3);
  const [speed, setSpeed] = useState(30);
  const [breakDuration, setBreakDuration] = useState(30);
  const [duration, setDuration] = useState(0);

  useEffect(() => {
    setDuration(calculateDuration());
  }, [number, sets, speed, breakDuration]);

  function handleInc() {
    const currentDuration = getDuration();
    const newDuration = Math.floor(currentDuration) + 1;
    setDuration(newDuration);
  }

  function handleDec() {
    const currentDuration = getDuration();
    const newDuration = Math.max(Math.floor(currentDuration) - 1, 0);
    setDuration(newDuration);
  }

  return (
    <div>
      <input type="number" value={number} onChange={(e) => setNumber(e.target.value)} />
      <input type="number" value={sets} onChange={(e) => setSets(e.target.value)} />
      <input type="number" value={speed} onChange={(e) => setSpeed(e.target.value)} />
      <input
        type="number"
        value={breakDuration}
        onChange={(e) => setBreakDuration(e.target.value)}
      />
      <p>Duration: {duration}</p>
      <button onClick={handleInc}>Increase</button>
      <button onClick={handleDec}>Decrease</button>
    </div>
  );
}
```

I hope this helps!

# Using Helper Functions In Effects

Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Play a sound whenever the duration state changes.

**Problem:**

- Playing the sound in event handlers and the effect causes duplicate sounds and state resets.
- Difficulty in understanding the interaction between hooks and reactive values.

**Solution:**

1. **Move playSound function to a separate effect:** Separate the sound-playing logic from the duration-updating logic.

```javascript
const playSound = (allowSound, clickSound) => {
  if (allowSound) {
    clickSound.play();
  }
};

useEffect(() => {
  playSound(allowSound, clickSound);
}, [duration, allowSound]);
```

2. **Avoid useCallback:** Instead of memorizing the playSound function, directly call it in the effect.

3. **Remove playSound calls from event handlers:** Since the sound is now played in the effect, remove the playSound calls from the event handlers.

```javascript
// Remove playSound calls from event handlers
```

4. **Declare duration in the effect's dependency array:** Even though duration is not used in the effect, declare it in the dependency array to trigger the effect whenever duration changes.

```javascript
useEffect(() => {
  playSound(allowSound, clickSound);
}, [duration, allowSound]);
```

**Benefits:**

- Clearer separation of concerns
- Improved understanding of hook interactions
- Elimination of duplicate sounds and state resets

**Code:**

```javascript
import React, { useState, useEffect } from 'react';

const calculateDuration = () => {
  // Calculate duration based on number, sets, speed, breakDuration
};

function App() {
  const [number, setNumber] = useState(1);
  const [sets, setSets] = useState(3);
  const [speed, setSpeed] = useState(30);
  const [breakDuration, setBreakDuration] = useState(30);
  const [duration, setDuration] = useState(0);
  const [allowSound, setAllowSound] = useState(true);
  const clickSound = new Audio('click.mp3');

  useEffect(() => {
    setDuration(calculateDuration());
  }, [number, sets, speed, breakDuration]);

  function handleInc() {
    const currentDuration = getDuration();
    const newDuration = Math.floor(currentDuration) + 1;
    setDuration(newDuration);
  }

  function handleDec() {
    const currentDuration = getDuration();
    const newDuration = Math.max(Math.floor(currentDuration) - 1, 0);
    setDuration(newDuration);
  }

  useEffect(() => {
    playSound(allowSound, clickSound);
  }, [duration, allowSound]);

  return (
    <div>
      <input type="number" value={number} onChange={(e) => setNumber(e.target.value)} />
      <input type="number" value={sets} onChange={(e) => setSets(e.target.value)} />
      <input type="number" value={speed} onChange={(e) => setSpeed(e.target.value)} />
      <input
        type="number"
        value={breakDuration}
        onChange={(e) => setBreakDuration(e.target.value)}
      />
      <p>Duration: {duration}</p>
      <button onClick={handleInc}>Increase</button>
      <button onClick={handleDec}>Decrease</button>
      <button onClick={() => setAllowSound(!allowSound)}>Toggle Sound</button>
    </div>
  );
}
```

# Closures in Effects

Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Understand the concept of stale closures in React hooks and how to avoid them.

**Problem:**

Effects that depend on state variables may not be updated properly if the dependency array is not specified correctly, leading to stale closures.

**Solution:**

- Specify all state variables that the effect depends on in the dependency array.
- Understand that the effect function will only capture the current snapshot of the specified state variables when it is executed.
- Avoid using state variables directly inside the effect function without specifying them in the dependency array.

**Key Points:**

- A stale closure occurs when a function captures outdated values from the time it was created.
- The dependency array tells React which state variables the effect needs to re-render when they change.
- Adding a state variable to the dependency array does not mean it will be used inside the effect function.

**Code:**

```javascript
import React, { useState, useEffect } from 'react';

const calculateDuration = () => {
  // Calculate duration based on number, sets, speed, breakDuration
};

function App() {
  const [number, setNumber] = useState(9);
  const [sets, setSets] = useState(5);
  const [speed, setSpeed] = useState(30);
  const [breakDuration, setBreakDuration] = useState(30);
  const [duration, setDuration] = useState(calculateDuration());

  useEffect(() => {
    document.title = `Your ${number} exercise workout`;
  }, [number]);

  useEffect(() => {
    setDuration(calculateDuration());
  }, [number, sets, speed, breakDuration]);

  useEffect(() => {
    console.log('Effect 2');
  }, []);

  function handleInc() {
    const currentDuration = getDuration();
    const newDuration = Math.floor(currentDuration) + 1;
    setDuration(newDuration);
  }

  function handleDec() {
    const currentDuration = getDuration();
    const newDuration = Math.max(Math.floor(currentDuration) - 1, 0);
    setDuration(newDuration);
  }

  return (
    <div>
      <input type="number" value={number} onChange={(e) => setNumber(e.target.value)} />
      <input type="number" value={sets} onChange={(e) => setSets(e.target.value)} />
      <input type="number" value={speed} onChange={(e) => setSpeed(e.target.value)} />
      <input
        type="number"
        value={breakDuration}
        onChange={(e) => setBreakDuration(e.target.value)}
      />
      <p>Duration: {duration}</p>
      <button onClick={handleInc}>Increase</button>
      <button onClick={handleDec}>Decrease</button>
    </div>
  );
}
```

**Additional Notes:**

* The `useRef` hook can be used to persist a value across renders without creating a stale closure.
* It is important to be mindful of the dependencies of effects to avoid unnecessary re-renders and maintain performance.

