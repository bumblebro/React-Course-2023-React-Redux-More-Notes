# What is the Context API?

### React Context API Notes

**Problem:**
Passing state down through multiple levels of a component tree can quickly become cumbersome and inconvenient, a problem known as prop drilling.

**Solution:**
The React Context API allows you to pass state from a parent component into a deeply nested child component without having to manually pass props down the component tree.

**How it works:**
The Context API has three main components:

1. **Provider:** A special React component that gives all child components access to a so-called value.
2. **Consumer:** A React component that reads the value from a provider.
3. **Context object:** An object that represents the context and is used to create the provider and consumer components.

To use the Context API, you first need to create a context object using the `createContext()` function. This function takes an optional default value for the context, which will be used if a component does not have a matching provider above it in the component tree.

Once you have created a context object, you can then create provider and consumer components. The provider component takes the context value as a prop and wraps all of the components that need access to the context state. The consumer component takes a function as a child, which is called with the current context value as an argument.

When a component is subscribed to a context, it will be re-rendered whenever the context value changes. This means that you can easily keep your components up-to-date with the latest state without having to manually pass props down the component tree.

**Example:**

```javascript
// Create a context object.
const ThemeContext = React.createContext({
  theme: "light",
});

// Create a provider component.
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Create a consumer component.
function ThemeConsumer() {
  const { theme } = React.useContext(ThemeContext);

  return <div style={{ color: theme }}>This is my content.</div>;
}

// Render the app.
function App() {
  return (
    <ThemeProvider>
      <ThemeConsumer />
    </ThemeProvider>
  );
}
```

In this example, the `ThemeConsumer` component will be re-rendered whenever the `theme` state variable changes. This means that the content of the `ThemeConsumer` component will always be displayed in the current theme.

### Benefits of using the Context API:

* It can help to reduce prop drilling and make your code more organized and maintainable.
* It can make it easier to share state across multiple components in your application.
* It can help you to create a more centralized state management system.

### Best practices for using the Context API:

* Only use the Context API for state that needs to be shared across multiple components in your application.
* Avoid using the Context API for state that only needs to be accessed within a single component.
* Create a separate file to define your context objects.
* Use descriptive names for your context objects and context values.
* Document your context objects and context values so that other developers can easily understand how to use them.

Overall, the React Context API is a powerful tool that can help you to write more maintainable and scalable React applications.

# Creating and Providing a Context

**Atomic Blog Application**

**Problem:** The Atomic Blog application has a lot of prop drilling.

**Solution:** Use the Context API to pass state from parent components to deeply nested child components without having to manually pass props down the component tree.

**Steps:**

1. Create a new context using the `createContext()` function.
2. Create a provider component that wraps all of the components that need access to the context state.
3. Pass the context value into the provider component as a prop.
4. Consume the context in all of the components that need access to the data using the `useContext()` hook.

**Example:**

```javascript
// Create a new context.
const PostContext = React.createContext({
  posts: [],
  onClearPosts: () => {},
  onAddPost: () => {},
  searchQuery: "",
});

// Create a provider component.
function PostProvider({ children }) {
  const [posts, setPosts] = useState([]);
  const [searchQuery, setSearchQuery] = useState("");

  const handleClearPosts = () => {
    setPosts([]);
  };

  const handleAddPost = () => {
    // Add a new post to the posts array.
  };

  return (
    <PostContext.Provider value={{ posts, onClearPosts, onAddPost, searchQuery }}>
      {children}
    </PostContext.Provider>
  );
}

// Consume the context in a child component.
function ListComponent() {
  const { posts } = useContext(PostContext);

  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

**Benefits of using the Context API:**

* It can help to reduce prop drilling and make your code more organized and maintainable.
* It can make it easier to share state across multiple components in your application.
* It can help you to create a more centralized state management system.

**Best practices for using the Context API:**

* Only use the Context API for state that needs to be shared across multiple components in your application.
* Avoid using the Context API for state that only needs to be accessed within a single component.
* Create a separate file to define your context objects.
* Use descriptive names for your context objects and context values.
* Document your context objects and context values so that other developers can easily understand how to use them.

Overall, the Context API is a powerful tool that can help you to write more maintainable and scalable React applications.

# Consuming the Context

**Removing Props with the Context API**

**Problem:** Prop drilling can make code cumbersome and difficult to maintain.

**Solution:** Use the Context API to pass state from parent components to deeply nested child components without having to manually pass props down the component tree.

**Steps:**

1. Create a context using the `createContext()` function.
2. Wrap the components that need access to the context state in a provider component.
3. Pass the context value into the provider component as a prop.
4. Consume the context in all of the components that need access to the data using the `useContext()` hook.

**Example:**

```javascript
// Create a context.
const PostContext = React.createContext({
  posts: [],
  onClearPosts: () => {},
  onAddPost: () => {},
  searchQuery: "",
});

// Create a provider component.
function PostProvider({ children }) {
  const [posts, setPosts] = useState([]);
  const [searchQuery, setSearchQuery] = useState("");

  const handleClearPosts = () => {
    setPosts([]);
  };

  const handleAddPost = () => {
    // Add a new post to the posts array.
  };

  return (
    <PostContext.Provider value={{ posts, onClearPosts, onAddPost, searchQuery }}>
      {children}
    </PostContext.Provider>
  );
}

// Consume the context in a child component.
function ListComponent() {
  const { posts } = useContext(PostContext);

  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

**Benefits of using the Context API:**

* It can help to reduce prop drilling and make your code more organized and maintainable.
* It can make it easier to share state across multiple components in your application.
* It can help you to create a more centralized state management system.

**Best practices for using the Context API:**

* Only use the Context API for state that needs to be shared across multiple components in your application.
* Avoid using the Context API for state that only needs to be accessed within a single component.
* Create a separate file to define your context objects.
* Use descriptive names for your context objects and context values.
* Document your context objects and context values so that other developers can easily understand how to use them.

**Benefits of refactoring the Atomic Blog application using the Context API:**

* The code is now more organized and maintainable.
* It is easier to share state across multiple components in the application.
* The components are more reusable and standalone.

**Improvements:**

* Extract the button and effect into their own components.
* Use memoization to prevent unnecessary re-renders.
* Use a more robust state management solution, such as Redux or Recoil.

# Advanced Pattern: A Custom Provider and Hook

**Detailed Notes with Code from the Paragraph Given**

**Problem:** The code for the Atomic Blog application is a bit messy, with the state and state updating logic spread across multiple components.

**Solution:** Refactor the code to create a custom Context Provider component and a custom hook for consuming the context. This will make the code more organized and maintainable, and it will also prevent developers from using the context value outside of the PostProvider.

**Code:**

```javascript
// Create a custom Context Provider component.
export function PostProvider({ children }) {
  const [posts, setPosts] = useState([]);
  const [searchQuery, setSearchQuery] = useState("");

  const handleClearPosts = () => {
    setPosts([]);
  };

  const handleAddPost = () => {
    // Add a new post to the posts array.
  };

  return (
    <PostContext.Provider value={{ posts, onClearPosts, onAddPost, searchQuery }}>
      {children}
    </PostContext.Provider>
  );
}

// Create a custom hook for consuming the context.
export function usePosts() {
  const context = useContext(PostContext);

  if (!context) {
    throw new Error("PostContext was used outside of the PostProvider.");
  }

  return context;
}
```

**Usage:**

```javascript
// Wrap all of the components that need access to the context in the PostProvider component.
<PostProvider>
  <List />
  <Search />
  <Header />
</PostProvider>

// Consume the context in the components that need it using the usePosts hook.
const { posts } = usePosts();
```

**Benefits:**

* The code is more organized and maintainable.
* The state and state updating logic is centralized in the PostProvider component.
* Developers are prevented from using the context value outside of the PostProvider.

# Thinking In React: Advanced State Management

**State Management in React**

## Types of State

* **Accessibility:** Local state or global state
* **Domain:** UI state or remote state

## State Placement Options

* **Local component:** useState, useReducer, useRef
* **Parent component:** Lift state up
* **Context:** Global UI state
* **Third-party state management library:** Redux, React Query, SWR, Zustand
* **URL:** Shareable and bookmarkable state
* **Local storage/session storage:** State stored in the user's browser

## Tools for Managing State

| State Type | Tools |
|---|---|---|
| Local UI state | useState, useReducer |
| Local remote state | fetch + useState/useReducer |
| Global remote state | Context API, Redux, React Query, SWR, RTK Query |
| Global UI state | Context API, Redux |

## Tips for Choosing the Right Tool

* For small applications, you can use a simple fetch inside a useEffect to load remote data and store it as state with useState or useReducer.
* For bigger applications, it's recommended to use a specialized tool for managing remote state, such as React Query, SWR, or RTK Query.
* For global UI state, the Context API coupled with useState or useReducer is a great tool. However, if you need something more performant, you can look into Redux.

## Conclusion

The best way to manage state in React depends on the specific needs of your application. However, the following general guidelines can be helpful:

* Use useState or useReducer for local UI state.
* Use a simple fetch inside a useEffect to load remote data and store it as state with useState or useReducer for local remote state in small applications.
* Use a specialized tool for managing remote state, such as React Query, SWR, or RTK Query, for global remote state in bigger applications.
* Use the Context API coupled with useState or useReducer for global UI state.
* Consider using Redux if you need a more performant solution for global UI state.

# Back to "WorldWise": Creating a CitiesContext

**Using the Context API in React**

**Detailed Notes with Code**

## Introduction

In this video, we will create a custom context provider component and hook for managing the cities data in the WorldWise application. This will allow us to get rid of some prop drilling and make the code more organized and maintainable.

## Code

```javascript
// Create a custom context provider component.
import { createContext, useState, useEffect } from "react";

const CitiesContext = createContext();

const CitiesProvider = ({ children }) => {
  const API_URL = "https://api.example.com/cities";

  const [cities, setCities] = useState([]);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    const fetchCities = async () => {
      const response = await fetch(API_URL);
      const json = await response.json();
      setCities(json.cities);
      setIsLoading(false);
    };

    fetchCities();
  }, []);

  return (
    <CitiesContext.Provider value={{ cities, isLoading }}>
      {children}
    </CitiesContext.Provider>
  );
};

// Create a custom hook for consuming the context.
const useCities = () => {
  const context = useContext(CitiesContext);

  if (!context) {
    throw new Error("CitiesContext was used outside of the CitiesProvider.");
  }

  return context;
};

// Usage:

// Wrap the application component in the CitiesProvider component.
<CitiesProvider>
  <App />
</CitiesProvider>

// Consume the context in any component using the useCities hook.
const App = () => {
  const { cities, isLoading } = useCities();

  // ...
};
```

## Benefits

* The code is more organized and maintainable.
* The state and state updating logic is centralized in the CitiesProvider component.
* Developers are prevented from using the context value outside of the CitiesProvider.
* The context can be consumed in any component without the need to pass props down the component tree.

**Conclusion**

The Context API is a powerful tool for managing state in React applications. By using custom context provider components and hooks, we can make our code more organized, maintainable, and scalable.

# Consuming the CitiesContext

**Detailed Notes with Code from the Paragraph Given**

## Refactoring the Application to Use the Context API

In this section, we will refactor the WorldWise application to use the Context API to manage the cities data. This will make the code more organized, maintainable, and scalable.

**Code:**

```javascript
// Create a custom hook for consuming the cities context.
import { useContext } from "react";
import { CitiesContext } from "./CitiesContext";

const useCities = () => {
  const context = useContext(CitiesContext);

  if (!context) {
    throw new Error("CitiesContext was used outside of the CitiesProvider.");
  }

  return context;
};

// Usage:

// Wrap the application component in the CitiesProvider component.
<CitiesProvider>
  <App />
</CitiesProvider>

// Consume the context in any component using the useCities hook.
const App = () => {
  const { cities, isLoading } = useCities();

  // ...
};
```

**Steps:**

1. Create a custom hook for consuming the cities context. This hook will take no arguments and return the current context value.
2. Import the useCities hook into the CityList and CountryList components.
3. Remove the cities and isLoading props from the CityList and CountryList components.
4. In the CityList and CountryList components, consume the cities and isLoading state from the useCities hook.
5. Reload the application and verify that it still works.

**Benefits:**

* The code is more organized and maintainable.
* The state and state updating logic is centralized in the CitiesProvider component.
* Developers are prevented from using the context value outside of the CitiesProvider.
* The context can be consumed in any component without the need to pass props down the component tree.

**Conclusion**

By refactoring the WorldWise application to use the Context API, we were able to make the code more organized, maintainable, and scalable. This makes it easier to understand and update the code in the future.

# Finishing the City View

**Detailed Notes with Code from the Paragraph Given**

## Using the Context API to Manage the City State

In this section, we will use the Context API to manage the city state in the WorldWise application. This will allow us to access the city data from any component in the application without the need to pass props down the component tree.

**Code:**

```javascript
// Create a context provider component for the city state.
import { createContext, useState, useEffect } from "react";

const CityContext = createContext();

const CityProvider = ({ children }) => {
  const [currentCity, setCurrentCity] = useState(null);
  const [isLoading, setIsLoading] = useState(true);

  const getCity = async (id) => {
    const response = await fetch(`/cities/${id}`);
    const city = await response.json();
    setCurrentCity(city);
    setIsLoading(false);
  };

  useEffect(() => {
    getCity(new URLSearchParams(window.location.search).get("id"));
  }, [window.location.search]);

  return (
    <CityContext.Provider value={{ currentCity, isLoading }}>
      {children}
    </CityContext.Provider>
  );
};

// Create a custom hook for consuming the city context.
import { useContext } from "react";
import { CityContext } from "./CityContext";

const useCity = () => {
  const context = useContext(CityContext);

  if (!context) {
    throw new Error("CityContext was used outside of the CityProvider.");
  }

  return context;
};

// Usage:

// Wrap the application component in the CityProvider component.
<CityProvider>
  <App />
</CityProvider>

// Consume the city context in any component using the useCity hook.
const City = () => {
  const { currentCity, isLoading } = useCity();

  // ...
};
```

**Benefits:**

* The city state is now centralized in the CityProvider component.
* Components can access the city state from anywhere in the application without the need to pass props down the component tree.
* The city state is updated automatically when the URL changes.

**Conclusion**

By using the Context API to manage the city state, we have made the WorldWise application more organized, maintainable, and scalable.

# Advanced State Management System: Context + useReducer

**Detailed notes with code from the paragraph given:**

**Introduction:**

The paragraph describes how to build an advanced state management system by combining the context API with a useReducer hook. This is a common pattern in React development, and it can be used to manage complex state in a centralized and efficient way.

**Reducer function:**

The reducer function is a pure function that takes the current state and an action object as input and returns a new state object. The action object contains information about the state change that should be made.

```javascript
const reducer = (state, action) => {
  switch (action.type) {
    case 'CITIES_LOADED':
      return {
        ...state,
        cities: action.payload,
        isLoading: false,
      };
    case 'CITY_LOADED':
      return {
        ...state,
        currentCity: action.payload,
      };
    case 'CITY_CREATED':
      return {
        ...state,
        cities: [...state.cities, action.payload],
      };
    case 'CITY_DELETED':
      return {
        ...state,
        cities: state.cities.filter(city => city.id !== action.payload),
      };
    default:
      throw new Error(`Unknown action type: ${action.type}`);
  }
};
```

**Initial state:**

The initial state is the state of the application before any actions have been dispatched. It should be a plain JavaScript object that contains all of the state data for the application.

```javascript
const initialState = {
  cities: [],
  isLoading: true,
  currentCity: {},
};
```

**useReducer hook:**

The useReducer hook takes a reducer function and an initial state as input and returns an array that contains the current state value and a dispatch function. The dispatch function can be used to dispatch actions to the reducer function.

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

**Using the dispatch function:**

The dispatch function can be used to dispatch actions to the reducer function. This will cause the reducer function to update the state of the application.

```javascript
dispatch({ type: 'CITIES_LOADED', payload: cities });
```

**Handling asynchronous data:**

When dealing with asynchronous data, it is important to remember that the reducer function must be a pure function. This means that it cannot perform any asynchronous operations.

To handle asynchronous data, you can use a separate function to fetch the data and then dispatch an action to the reducer function once the data has been received.

```javascript
async function fetchCities() {
  const response = await fetch('/cities');
  const cities = await response.json();
  dispatch({ type: 'CITIES_LOADED', payload: cities });
}
```

**Conclusion:**

By combining the context API with a useReducer hook, you can create a powerful and flexible state management system for your React applications. This can help you to keep your code organized and maintainable, and it can also improve the performance of your applications.

# Adding Fake Authentication: Setting Up Context

**Detailed notes with code from the paragraph given:**

## Introduction

The paragraph describes how to implement a fake authentication system in a React application using a context API. This is a useful pattern for implementing authentication in React applications, as it allows you to centralize your authentication logic and make it accessible to all parts of your application.

## Fake authentication

The paragraph explains that the fake authentication system will use a hardcoded user object instead of making an API call to verify the user's credentials. This is just to demonstrate the basics of authentication in React, and a real authentication system would typically make an API call to verify the user's credentials.

## Context API

The paragraph explains that the context API will be used to store the user state and authentication state, and to make these states accessible to all parts of the application. This is done by creating a context provider and a custom hook.

## Code

The following code shows how to implement the fake authentication system using a context API:

```javascript
// AuthContext.js

import React, { createContext, useReducer } from 'react';

const AuthContext = createContext();

const initialState = {
  user: null,
  isAuthenticated: false,
};

const reducer = (state, action) => {
  switch (action.type) {
    case 'LOGIN':
      return {
        ...state,
        user: action.payload,
        isAuthenticated: true,
      };
    case 'LOGOUT':
      return {
        ...state,
        user: null,
        isAuthenticated: false,
      };
    default:
      throw new Error('Unknown action type: ${action.type}');
  }
};

const AuthProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <AuthContext.Provider value={{ ...state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = React.useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }

  return context;
};

export default AuthContext;
```

## Usage

The `AuthProvider` component should be wrapped around the entire application. This will make the user state and authentication state available to all parts of the application.

To use the authentication system, you can use the `useAuth` hook. This hook will return an object containing the user state and authentication state.

Here is an example of how to use the `useAuth` hook to implement a login button:

```javascript
import { useAuth } from './AuthContext';

const LoginButton = () => {
  const { login } = useAuth();

  return (
    <button onClick={() => login('user@email.com', 'password')}>
      Login
    </button>
  );
};
```

When the user clicks the login button, the `login` function will be called, which will dispatch the `LOGIN` action to the reducer. The reducer will then update the user state and authentication state.

## Conclusion

This is a basic example of how to implement a fake authentication system in a React application using a context API. A real authentication system would typically make an API call to verify the user's credentials.

# Adding Fake Authentication: Implementing "Login"

**Detailed notes with code from the paragraph given:**

## Introduction

The paragraph describes how to implement the login and logout functionalities in the application using a context API.

## Fake login

The paragraph explains that the fake login function will simply check if the email and password are equal to the hardcoded user object. If they are, then the login function will dispatch the `LOGIN` action to the reducer, which will update the user state and authentication state.

## Logout

The paragraph explains that the logout function will simply dispatch the `LOGOUT` action to the reducer, which will set the user state to null and the authentication state to false.

## Code

The following code shows how to implement the login and logout functionalities using a context API:

```javascript
// AuthContext.js

import React, { createContext, useReducer } from 'react';

const AuthContext = createContext();

const initialState = {
  user: null,
  isAuthenticated: false,
};

const reducer = (state, action) => {
  switch (action.type) {
    case 'LOGIN':
      return {
        ...state,
        user: action.payload,
        isAuthenticated: true,
      };
    case 'LOGOUT':
      return {
        ...state,
        user: null,
        isAuthenticated: false,
      };
    default:
      throw new Error('Unknown action type: ${action.type}');
  }
};

const AuthProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <AuthContext.Provider value={{ ...state, dispatch }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = React.useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }

  return context;
};

export default AuthContext;
```

**Login**

The following code shows how to use the `useAuth` hook to implement a login button:

```javascript
import { useAuth } from './AuthContext';

const LoginButton = () => {
  const { login } = useAuth();

  return (
    <button onClick={() => login('user@email.com', 'password')}>
      Login
    </button>
  );
};
```

**Logout**

The following code shows how to use the `useAuth` hook to implement a logout button:

```javascript
import { useAuth } from './AuthContext';

const LogoutButton = () => {
  const { logout } = useAuth();

  return (
    <button onClick={() => logout()}>
      Logout
    </button>
  );
};
```

**Handling re-render**

When the user logs in or out, the user state and authentication state will change. This will cause the application to re-render. To handle this re-render, you can use a `useEffect` hook to check the user state and authentication state and navigate to the appropriate page.

```javascript
import { useEffect } from 'react';
import { useAuth } from './AuthContext';

const App = () => {
  const { isAuthenticated } = useAuth();

  useEffect(() => {
    if (isAuthenticated) {
      // Navigate to the app page
    } else {
      // Navigate to the login page
    }
  }, [isAuthenticated]);

  // ...
};
```

**Preventing the user from going back to the login page after logging out**

When the user logs out, you want to prevent them from going back to the login page. To do this, you can use the `replace` option when navigating to the app page.

```javascript
import { useNavigate } from 'react-router-dom';
import { useAuth } from './AuthContext';

const App = () => {
  const { isAuthenticated } = useAuth();
  const navigate = useNavigate();

  useEffect(() => {
    if (isAuthenticated) {
      // Navigate to the app page with the replace option set to true
      navigate('/', { replace: true });
    } else {
      // Navigate to the login page
      navigate('/login');
    }
  }, [isAuthenticated]);

  // ...
};
```

## Conclusion

This is a basic example of how to implement the login and logout functionalities in a React application using a context API.

# Adding Fake Authentication: Protecting a Route

**Summary of the paragraph:**

The third part of the authentication flow is to protect the application against unauthorized access. This is done by redirecting the user back to the homepage whenever they reach a route that they should not reach when they are not logged in.

To implement this functionality, a specialized component called `ProtectedRoute` is created. This component wraps the entire application and checks whether the user is authenticated before rendering it. If the user is not authenticated, the user is redirected to the homepage.

The `ProtectedRoute` component is used by wrapping the `appLayout` component in the `App.jsx` file. This ensures that all routes in the application are protected against unauthorized access.

**Detailed notes with code:**

**ProtectedRoute.jsx:**

```javascript
import React from "react";
import { useAuth } from "./auth";
import { useNavigate } from "react-router-dom";

const ProtectedRoute = ({ children }) => {
  const isAuthenticated = useAuth();
  const navigate = useNavigate();

  // Redirect the user to the homepage if they are not authenticated.
  if (!isAuthenticated) {
    navigate("/");
    return null;
  }

  // Otherwise, render the children.
  return children;
};

export default ProtectedRoute;
```

**App.jsx:**

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
import ProtectedRoute from "./ProtectedRoute";
import AppLayout from "./AppLayout";

const App = () => {
  return (
    <Router>
      <ProtectedRoute>
        <AppLayout />
      </ProtectedRoute>
    </Router>
  );
};

export default App;
```

**How to use the ProtectedRoute component:**

To use the `ProtectedRoute` component, simply wrap any route that you want to protect in it. For example, to protect the `/cities` route, you would do the following:

```javascript
import React from "react";
import { Route } from "react-router-dom";
import ProtectedRoute from "./ProtectedRoute";
import CitiesPage from "./CitiesPage";

const CitiesRoute = () => {
  return (
    <ProtectedRoute>
      <CitiesPage />
    </ProtectedRoute>
  );
};

export default CitiesRoute;
```

Any user who tries to access the `/cities` route without being authenticated will be redirected to the homepage.

# 
