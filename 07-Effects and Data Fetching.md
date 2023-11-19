# The Component Lifecycle

**Key takeaways from the lecture on the component lifecycle:**

* A component lifecycle encompasses the different phases that a component instance can go through over time.
* The three phases of the component lifecycle are mounting, re-rendering, and unmounting.
* Mounting is the process of rendering a component for the first time.
* Re-rendering is the process of updating a component's render output based on a change in its state or props.
* Unmounting is the process of removing a component from the DOM.

**Code:**

```javascript
// Component lifecycle methods

// Mounting
componentDidMount() {
  // Executed after the component is mounted.
}

// Re-rendering
componentDidUpdate(prevProps, prevState) {
  // Executed after the component is re-rendered.
}

// Unmounting
componentWillUnmount() {
  // Executed before the component is unmounted.
}

// useEffect hook

useEffect(callback, [dependencies]) {
  // Executed after the component is mounted and on every re-render.
}
```

**Example:**

```javascript
// Component that logs its state and props on mount and unmount.

function MyComponent({ name }) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('State:', count);
    console.log('Props:', name);
  }, [count, name]);

  componentDidMount() {
    console.log('Mounted!');
  }

  componentWillUnmount() {
    console.log('Unmounted!');
  }

  return <div>{count}</div>;
}
```

**Output:**

```
Mounted!
State: 0
Props: John Doe

// User clicks a button to increment the count.

State: 1
Props: John Doe

// User navigates to a different page, and the component is unmounted.

Unmounted!
```

The component lifecycle is an important concept to understand in React, as it allows us to hook into different phases of the lifecycle to execute code at specific points in time. This can be useful for a variety of tasks, such as fetching data, setting up timers, and cleaning up resources.

# How NOT to Fetch Data in React
**Key takeaways from the lecture on fetching data in React:**

* **Fetch data outside of render logic:** It is never allowed to fetch data inside of render logic, as this can lead to infinite loops and performance problems. Instead, fetch data in a separate function or hook, such as useEffect.
* **Use the fetch API:** The fetch API is a standard JavaScript API for making HTTP requests. It is a good choice for fetching data from APIs in React.
* **Handle errors:** It is important to handle errors gracefully when fetching data. This can be done by using the `catch()` method on the fetch promise.

**Code:**

```javascript
// Fetch data outside of render logic
const fetchMovies = async () => {
  const response = await fetch('https://www.omdbapi.com/?s=interstellar&apikey=YOUR_API_KEY');
  const data = await response.json();
  return data.search;
};

// Use the useEffect hook to fetch data and set state
useEffect(() => {
  const movies = await fetchMovies();
  setMovies(movies);
}, []);
```

This code will fetch data from the OMDb API when the component mounts. The data will then be stored in the `movies` state variable. The `useEffect` hook ensures that the data is only fetched once, even if the component re-renders.

**Error handling:**

To handle errors, we can use the `catch()` method on the fetch promise:

```javascript
const fetchMovies = async () => {
  try {
    const response = await fetch('https://www.omdbapi.com/?s=interstellar&apikey=YOUR_API_KEY');
    const data = await response.json();
    return data.search;
  } catch (error) {
    // Handle error here
  }
};
```

If an error occurs, the `catch()` block will be executed. We can then log the error to the console, display a message to the user, or take any other necessary action.

# useEffect to the Rescue

**Summary of the lecture on the useEffect hook:**

The useEffect hook allows us to execute side effects after a component has been rendered. This is useful for tasks such as fetching data, setting up timers, and cleaning up resources.

**Code:**

```javascript
// Use the useEffect hook to fetch data on mount
useEffect(() => {
  const movies = await fetchMovies();
  setMovies(movies);
}, []);
```

The first argument to the useEffect hook is a function that contains the side effect that we want to execute. The second argument is a dependency array. If the dependency array is empty, the effect will only be executed on mount.

**Benefits of using useEffect to fetch data:**

* It prevents infinite loops and performance problems.
* It makes the code more readable and organized.
* It is more scalable and reusable than other methods of fetching data.

**Example:**

The following code shows how to use the useEffect hook to fetch data from the OMDb API on mount:

```javascript
const fetchMovies = async () => {
  const response = await fetch('https://www.omdbapi.com/?s=interstellar&apikey=YOUR_API_KEY');
  const data = await response.json();
  return data.search;
};

useEffect(() => {
  const movies = await fetchMovies();
  setMovies(movies);
}, []);
```

This code will fetch data from the OMDb API when the component mounts and store the data in the `movies` state variable.

**Conclusion:**

The useEffect hook is a powerful tool for managing side effects in React applications. It is especially useful for fetching data on mount.

# A First Look at Effects

**Key takeaways from the lecture on effects and event handlers:**

* **Effects:** Effects are a way to execute side effects in React applications. They can be used to fetch data, set up timers, and clean up resources. Effects are executed at different moments of the component lifecycle, such as mounting, re-rendering, and unmounting.
* **Event handlers:** Event handlers are functions that are triggered when a specific event occurs, such as a click or a scroll. Event handlers are the preferred way to create side effects in React applications.

**Comparing effects and event handlers:**

| Characteristic | Effect | Event handler |
|---|---|---|
| Purpose | To keep a component in sync with the external world. | To react to a specific event in the user interface. |
| When to use | When the side effect needs to be executed at a specific moment of the component lifecycle, such as mounting or re-rendering. | When the side effect needs to be executed in response to a specific event in the user interface. |
| Example | Fetching data from an API on mount. | Updating a state variable when a button is clicked. |

**Best practices:**

* Always use event handlers to create side effects whenever possible.
* Only use the useEffect hook when you need to execute a side effect at a specific moment of the component lifecycle, such as mounting or re-rendering.

**Conclusion:**

Effects and event handlers are two powerful tools for managing side effects in React applications. It is important to understand the difference between the two and to use the right tool for the job.

# Using an async Function

**Summary of the video on converting effects to async functions:**

* We cannot directly use an async function as an effect callback because it returns a promise.
* Instead, we can create a new function inside the effect callback and make it async.
* When setting state in an effect callback, we need to use the updated state value instead of the stale state value.
* In React 18 strict mode, effects are called twice. This is to identify any problems with the effects.

**Code:**

```javascript
// Convert the effect callback to an async function
useEffect(() => {
  const fetchMovies = async () => {
    const res = await fetch('https://www.omdbapi.com/?s=interstellar&apikey=YOUR_API_KEY');
    const data = await res.json();
    setMovies(data.Search);
  };

  fetchMovies();
}, []);

// Use the updated state value in the effect callback
useEffect(() => {
  console.log(movies);
}, [movies]);
```

**Conclusion:**

Converting effects to async functions can make the code more readable and maintainable. However, it is important to be aware of the potential pitfalls, such as stale state and multiple effect calls in React 18 strict mode.

# Adding a Loading State
**Summary of the video on adding a loading indicator:**

* To add a loading indicator, we need to create a new state variable called `isLoading`.
* We set `isLoading` to `true` before fetching the data and set it back to `false` after the data has been fetched.
* We use the `isLoading` state variable to conditionally render the loading indicator or the movie list.

**Code:**

```javascript
// Create a new state variable to indicate whether the data is loading
const [isLoading, setIsLoading] = useState(false);

// Set isLoading to true before fetching the data
useEffect(() => {
  const fetchMovies = async () => {
    setIsLoading(true);

    const res = await fetch('https://www.omdbapi.com/?s=interstellar&apikey=YOUR_API_KEY');
    const data = await res.json();

    setMovies(data.Search);
    setIsLoading(false);
  };

  fetchMovies();
}, []);

// Conditionally render the loading indicator or the movie list
return (
  <>
    {isLoading && <Loader />}
    {!isLoading && <MovieList movies={movies} />}
  </>
);

// Loader component
const Loader = () => {
  return <p className="Loader">Loading...</p>;
};
```

**Conclusion:**

Adding a loading indicator to our application makes the user experience more natural and real-world. It also helps to prevent the user from thinking that the application is frozen or broken.

# Handling Errors

**Detailed notes with code from the given paragraph:**

## Handling errors in data fetching

When fetching data in a web application, we need to assume that something can always go wrong. This includes things like the user losing their internet connection, the API being unavailable, or the data being corrupted.

React does not have built-in error handling for fetch, so we need to implement it manually. To do this, we can use a try-catch block.

```javascript
try {
  // Fetch the data
  const response = await fetch('https://api.example.com/movies');

  // Check if the response was successful
  if (!response.ok) {
    throw new Error('Failed to fetch movies');
  }

  // Get the data from the response
  const data = await response.json();

  // Render the data
  // ...
} catch (error) {
  // Handle the error
  // ...
}
```

## Displaying error messages

Once we have caught an error, we can display a message to the user. To do this, we can use a state variable to store the error message and then render it conditionally.

```javascript
const [error, setError] = useState(null);

// Fetch the data
try {
  // ...
} catch (error) {
  setError(error.message);
}

// Render the error message
if (error) {
  <div className="error">{error}</div>;
}
```

## Handling specific errors

In some cases, we may want to handle specific errors in different ways. For example, if we are fetching data from an API that returns a special error code when no results are found, we can throw our own error to handle this case specifically.

```javascript
const [error, setError] = useState(null);

// Fetch the data
try {
  // ...

  // Check if the response indicates that no results were found
  if (response.status === 404) {
    throw new Error('Movie not found');
  }

  // Get the data from the response
  const data = await response.json();

  // Render the data
  // ...
} catch (error) {
  setError(error.message);
}

// Render the error message
if (error) {
  <div className="error">{error}</div>;
}
```

## Conclusion

Error handling is an important part of any web application. By following the tips above, we can ensure that our applications are resilient to errors and that users are always presented with a clear and informative message when something goes wrong.
# The useEffect Dependency Array
**Detailed notes with code from the given paragraph:**

## What is the dependency array in useEffect?

The dependency array in useEffect is a list of values that the effect depends on. If any of these values change, the effect will be re-executed. This is important because it prevents the effect from running on every render, which can improve performance and avoid stale closures.

## Why is the dependency array important?

The dependency array is important because it allows React to know when to re-execute the effect. Without the dependency array, React would not know when to re-execute the effect, and it would run on every render. This could lead to performance problems, and it could also cause stale closures.

## What are the different types of dependency arrays?

There are three different types of dependency arrays:

1. **Empty array:** An empty dependency array means that the effect will only run on mount.
2. **Non-empty array:** A non-empty dependency array means that the effect will run on mount and on every re-render where one of the dependencies in the array changes.
3. **No array:** No dependency array means that the effect will run on every render. This is generally not recommended, as it can lead to performance problems and stale closures.

## When are effects executed?

Effects are executed asynchronously after the render has been painted to the screen. This is to prevent effects from blocking the render process, which would cause users to see an old version of the component for too long.

## Example

Here is an example of a useEffect hook with a dependency array:

```javascript
const [title, setTitle] = useState('Interstellar');

useEffect(() => {
  document.title = title;
}, [title]);
```

This effect will run on mount and on every re-render where the `title` state variable changes. This will ensure that the document title is always in sync with the `title` state variable.

## Conclusion

The dependency array is a powerful tool that can be used to improve the performance and reliability of effects. By carefully specifying the dependencies in the array, we can ensure that effects only run when necessary and that they do not cause stale closures.

# Synchronizing Queries With Movie Data

**Detailed notes with code from the given paragraph:**

**Summary:**

This paragraph discusses how to use React effects to synchronize the search query with the movie search results. The author creates a few experiments to demonstrate how effects work and how to use them effectively. In the end, the author implements the basic functionality of synchronizing the search query with the movie search results.

**Code:**

```javascript
// React effect to synchronize the search query with the movie search results
useEffect(() => {
  if (query.length === 0 || query.length < 3) {
    // If the search query is empty or less than 3 characters, reset the movies state
    setMovies([]);
    setError('');
    return;
  }

  // Fetch movies based on the search query
  fetchMovies(query);
}, [query]);

// Fetch movies from the API
async function fetchMovies(query) {
  try {
    const response = await fetch(`https://api.example.com/movies?q=${query}`);
    const movies = await response.json();

    // Set the movies state with the fetched movies
    setMovies(movies);
  } catch (error) {
    // Set the error state with the error message
    setError(error.message);
  }
}
```

**Explanation:**

The effect above is synchronized with the `query` state variable, which means that it will be executed whenever the `query` state changes. This is because the `query` state variable is included in the dependency array of the effect.

When the effect is executed, it first checks if the search query is empty or less than 3 characters. If it is, then the movies state is reset and the error state is cleared. This is to prevent the API from being called with an empty or very short search query, which would result in a lot of irrelevant results.

If the search query is not empty or less than 3 characters, then the effect calls the `fetchMovies()` function to fetch movies from the API based on the search query. The fetched movies are then set in the movies state.

If any error occurs while fetching the movies, then the error state is set with the error message.

**Example usage:**

```javascript
// App component
const App = () => {
  const [query, setQuery] = useState('');
  const [movies, setMovies] = useState([]);
  const [error, setError] = useState('');

  useEffect(() => {
    if (query.length === 0 || query.length < 3) {
      setMovies([]);
      setError('');
      return;
    }

    fetchMovies(query);
  }, [query]);

  async function fetchMovies(query) {
    try {
      const response = await fetch(`https://api.example.com/movies?q=${query}`);
      const movies = await response.json();

      setMovies(movies);
    } catch (error) {
      setError(error.message);
    }
  }

  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />
      <ul>
        {movies.map((movie) => (
          <li key={movie.id}>{movie.title}</li>
        ))}
      </ul>
      {error && <p>Error: {error}</p>}
    </div>
  );
};
```

In this example, the `App` component uses the `query` state variable to store the search query and the `movies` state variable to store the fetched movies. The `useEffect` hook is used to synchronize the search query with the movie search results.

When the user types a new search query, the `query` state variable is updated. The `useEffect` hook then detects the change in the `query` state variable and executes the effect. The effect calls the `fetchMovies()` function to fetch movies from the API based on the search query. The fetched movies are then set in the `movies` state variable.

If any error occurs while fetching the movies, then the `error` state variable is set with the error message.

**Conclusion:**

This paragraph provides a good overview of how to use React effects to synchronize state with external data sources. The example code is clear and easy to understand.

# Selecting a Movie

**Detailed notes with code from the given paragraph:**

**Summary:**

This paragraph discusses how to add the ability to select a movie in a React application. The author creates a new component to display the selected movie and a new function to handle the selection of a movie. The author also discusses how to close the movie detail and how to fetch the movie that corresponds to the selected ID.

**Code:**

```javascript
// New component to display the selected movie
function MovieDetails({ selectedId }) {
  if (!selectedId) {
    return null;
  }

  return (
    <div className="detail">
      Selected ID: {selectedId}
    </div>
  );
}

// New function to handle the selection of a movie
function handleSelectMovie(movieId) {
  setSelectedId(movieId);
}

// Close the movie detail
function handleCloseMovie() {
  setSelectedId(null);
}

// Update the selected ID based on the current one
setSelectedId((previousSelectedId, id) => {
  if (id === previousSelectedId) {
    return null;
  }
  return id;
});
```

**Usage:**

```javascript
// Parent component
const App = () => {
  const [selectedId, setSelectedId] = useState(null);

  return (
    <div>
      <MovieList
        movies={movies}
        onSelectMovie={handleSelectMovie}
      />
      {selectedId && <MovieDetails selectedId={selectedId} />}

      <button className="btn-back" onClick={handleCloseMovie}>
        &larr;
      </button>
    </div>
  );
};

// Child component
const MovieList = ({ movies, onSelectMovie }) => {
  return (
    <ul className="list-of-movies">
      {movies.map((movie) => (
        <Movie
          key={movie.imdbID}
          movie={movie}
          onSelectMovie={onSelectMovie}
        />
      ))}
    </ul>
  );
};
```

**Conclusion:**

This paragraph provides a good overview of how to add the ability to select a movie in a React application. The example code is clear and easy to understand.

# Loading Movie Details

**Detailed notes with code from the given paragraph:**

**Summary:**

This paragraph discusses how to load movie details for individual movies in a React application. The author creates an effect to fetch the movie details whenever the selected ID changes. The author also discusses how to handle the delay between the click and the loading of the movie details by showing a loading indicator.

**Code:**

```javascript
// New state variable to track if the movie is loading
const [isLoading, setIsLoading] = useState(false);

// Effect to fetch the movie details whenever the selected ID changes
useEffect(() => {
  async function fetchMovieDetails() {
    const response = await fetch(`/api/movies/${selectedId}`);
    const movie = await response.json();

    setMovie(movie);
    setIsLoading(false);
  }

  // Fetch the movie details if the selected ID has changed
  if (selectedId) {
    setIsLoading(true);
    fetchMovieDetails();
  }
}, [selectedId]);

// Loading indicator
if (isLoading) {
  return <div>Loading...</div>;
}

// Render the movie details
return (
  <div className="movie-details">
    <img src={movie.poster} alt={movie.title} />
    <h2>{movie.title}</h2>
    <p>{movie.plot}</p>
    <p>Starring: {movie.actors}</p>
    <p>Directed by: {movie.director}</p>

    <StarRating rating={movie.imdbRating} maxRating={10} size={24} />
  </div>
);
```

**Example usage:**

```javascript
// App component
const App = () => {
  const [selectedId, setSelectedId] = useState(null);
  const [movie, setMovie] = useState({});

  return (
    <div>
      <MovieList
        movies={movies}
        onSelectMovie={setSelectedId}
      />
      <MovieDetails selectedId={selectedId} movie={movie} />
    </div>
  );
};
```

**Conclusion:**

This paragraph provides a good overview of how to load movie details for individual movies in a React application. The example code is clear and easy to understand.

#  Adding a Watched Movie

**Detailed notes with code from the given paragraph:**

**Summary:**

This paragraph discusses how to add watched movies to a list in a React application. The author creates a new function to add a movie to the list and passes it to the MovieDetails component. The author also adds a new state variable to track the user's rating of the movie and passes it to the StarRating component. Finally, the author discusses how to prevent the user from adding the same movie to the list multiple times.

**Code:**

```javascript
// New function to add a movie to the watched list
function handleAddWatch(movie) {
  // Create a new watched movie object
  const newWatchedMovie = {
    imdbID: movie.imdbID,
    title: movie.title,
    year: movie.year,
    poster: movie.poster,
    imdbRating: movie.imdbRating,
    userRating: movie.userRating,
    runtime: parseInt(movie.runtime.split(' ')[0]),
  };

  // Add the new movie to the watched list
  setWatched((watched) => [...watched, newWatchedMovie]);

  // Close the movie details
  handleCloseMovie();
}

// New state variable to track the user's rating of the movie
const [userRating, setUserRating] = useState('');

// Pass the watched array and the user rating state to the MovieDetails component
<MovieDetails
  selectedId={selectedId}
  watched={watched}
  onSetRating={setUserRating}
  onAddWatched={handleAddWatch}
/>
```

**Preventing the user from adding the same movie to the list multiple times:**

```javascript
// Check if the movie is already in the watched list
const isMovieInWatchedList = (movie) => {
  return watched.find((watchedMovie) => watchedMovie.imdbID === movie.imdbID);
};

// Update the MovieDetails component to disable the add button if the movie is already in the watched list
<MovieDetails
  selectedId={selectedId}
  watched={watched}
  onSetRating={setUserRating}
  onAddWatched={handleAddWatch}
  isMovieInWatchedList={isMovieInWatchedList}
/>
```

With these changes, the user will only be able to add a movie to the watched list once.

# Adding a New Effect: Changing Page Title

**Detailed notes with code from the given paragraph:**

**Summary:**

This paragraph discusses how to change the page title in the browser to the movie that is currently being watched in a React application. The author uses the `useEffect` hook to register a side effect that will be executed when the component mounts and when the `title` variable changes. The author also handles the case where the `title` variable is undefined when the component first mounts.

**Code:**

```javascript
// Import the useEffect hook
import { useEffect } from 'react';

// Add a new state variable to track the title of the movie
const [title, setTitle] = useState('');

// Implement the useEffect hook to change the page title
useEffect(() => {
  // Change the page title
  document.title = `Movie: ${title}`;

  // Cleanup function to reset the page title to the default value
  return () => {
    document.title = 'usePopcorn';
  };
}, [title]);

// Update the title of the movie when the component mounts
useEffect(() => {
  // Get the title of the movie from the API
  const getMovieTitle = async () => {
    const response = await fetch(`/api/movies/${selectedId}`);
    const movie = await response.json();
    setTitle(movie.title);
  };

  // Call the getMovieTitle function
  getMovieTitle();
}, [selectedId]);
```

**Handling the case where the `title` variable is undefined when the component first mounts:**

```javascript
// Add a conditional statement to the useEffect hook to prevent the page title from being changed to undefined
useEffect(() => {
  // If the title is undefined, return early
  if (!title) {
    return;
  }

  // Change the page title
  document.title = `Movie: ${title}`;

  // Cleanup function to reset the page title to the default value
  return () => {
    document.title = 'usePopcorn';
  };
}, [title]);
```

**Preventing the page title from staying the same when the user navigates back:**

```javascript
// Add a conditional statement to the useEffect hook to reset the page title if the selected movie is null
useEffect(() => {
  // If the selected movie is null, reset the page title
  if (!selectedId) {
    document.title = 'usePopcorn';
  }

  // Change the page title to the title of the selected movie
  document.title = `Movie: ${title}`;

  // Cleanup function to reset the page title to the default value
  return () => {
    document.title = 'usePopcorn';
  };
}, [selectedId, title]);
```

With these changes, the page title will be changed to the title of the movie that is currently being watched. The page title will also be reset to the default value when the user navigates back or when the selected movie is null.

# The useEffect Cleanup Function

**Notes on the useEffect cleanup function**

The useEffect cleanup function is a function that can be returned from a useEffect hook. It is used to clean up any side effects that were created in the effect. The cleanup function is executed in two cases:

* Before the effect is executed again, in order to clean up the results of the previous side effect.
* After the component instance has unmounted, in order to give us the opportunity to reset the side effect that we created, if that's necessary.

**When to use a cleanup function**

You should use a cleanup function whenever the side effect keeps happening after the component has been re-rendered or unmounted. For example, if you are making an HTTP request in your effect, you should use a cleanup function to cancel the request if the component re-renders or unmounts before the request completes. Other examples include:

* Canceling subscriptions to API services
* Stopping timers
* Removing event listeners

**Best practices for using cleanup functions**

* Each effect should only do one thing. If you need to create multiple effects in your components, use multiple useEffect hooks. This makes each effect easier to understand and clean up.
* Return the cleanup function from the useEffect hook. This ensures that the cleanup function is executed before the effect is executed again or before the component unmounts.
* In the cleanup function, undo any changes that were made in the effect. This will help to prevent memory leaks and other unwanted behaviors.

**Code example**

The following code example shows how to use a cleanup function to cancel an HTTP request:

```javascript
import { useEffect, useState } from "react";

const MovieDetails = () => {
  const [movie, setMovie] = useState();

  useEffect(() => {
    const fetchMovie = async () => {
      const response = await fetch("/api/movies/1");
      const data = await response.json();
      setMovie(data);
    };

    fetchMovie();

    // Return a cleanup function to cancel the request if the component unmounts
    return () => {
      fetchMovie.abort();
    };
  }, []);

  return (
    <div>
      <h1>{movie?.title}</h1>
    </div>
  );
};
```

In this example, the useEffect hook is used to fetch a movie from an API. The cleanup function is used to cancel the request if the component unmounts before the request completes. This prevents the request from continuing to run even after the component is no longer needed.

## Conclusion

The useEffect cleanup function is a powerful tool for managing side effects in React components. By using cleanup functions, you can prevent memory leaks and other unwanted behaviors.

# Cleaning Up the Title

**Detailed notes on the useEffect cleanup function**

In the paragraph you provided, the speaker is discussing how to use the useEffect cleanup function to solve the problem of the page title not being reset when the MovieDetails component is unmounted.

**What is the cleanup function?**

The cleanup function is an optional function that can be returned from a useEffect hook. It is used to clean up any side effects that were created in the effect. The cleanup function is executed in two cases:

* Before the effect is executed again, in order to clean up the results of the previous side effect.
* After the component instance has unmounted, in order to give us the opportunity to reset the side effect that we created, if that's necessary.

**When to use the cleanup function**

You should use the cleanup function whenever the side effect keeps happening after the component has been re-rendered or unmounted. For example, if you are making an HTTP request in your effect, you should use the cleanup function to cancel the request if the component re-renders or unmounts before the request completes. Other examples include:

* Canceling subscriptions to API services
* Stopping timers
* Removing event listeners

**How to use the cleanup function**

To use the cleanup function, simply return it from the useEffect hook. For example:

```javascript
useEffect(() => {
  // Create a side effect

  // Return a cleanup function
  return () => {
    // Clean up the side effect
  };
}, []);
```

**Example of using the cleanup function to reset the page title**

In the example below, the cleanup function is used to reset the page title when the MovieDetails component is unmounted:

```javascript
const MovieDetails = () => {
  const [movie, setMovie] = useState();

  useEffect(() => {
    // Fetch a movie from an API

    // Set the page title
    document.title = movie.title;

    // Return a cleanup function to reset the page title
    return () => {
      document.title = "usePopcorn";
    };
  }, [movie]);

  return (
    <div>
      <h1>{movie?.title}</h1>
    </div>
  );
};
```

In this example, the cleanup function sets the page title back to "usePopcorn" when the MovieDetails component is unmounted. This ensures that the page title is always reset when the user navigates to a different page.

**Closures and the cleanup function**

The speaker also discusses the concept of closures in JavaScript. A closure is a function that has access to the variables that were in scope when the function was created.

The cleanup function is executed after the component has been unmounted, which means that all of the state variables for the component have been destroyed. However, the cleanup function is still able to access the title variable because of the closure.

The cleanup function is closed over the title variable, which means that it has access to the value of the title variable even after the component has been unmounted.

**How to use the cleanup function between renders**

The speaker also mentions that the cleanup function runs between renders. This means that the cleanup function is executed after each time the component is re-rendered.

This can be useful for cleaning up side effects that are created in the effect. For example, if you are subscribing to an API in your effect, you can use the cleanup function to unsubscribe from the API when the component is re-rendered.

**Conclusion**

The useEffect cleanup function is a powerful tool for managing side effects in React components. By using the cleanup function, you can prevent memory leaks and other unwanted behaviors.

# Cleaning Up Data Fetching

**Detailed notes on the closure and the cleanup function**

**What is a closure?**

A closure in JavaScript is a function that has access to the variables in the scope where it was created, even after that scope has closed. This means that a closure can retain access to variables that would otherwise be garbage collected.

**How does the closure affect the cleanup function?**

The cleanup function in React is a function that is returned from a useEffect hook. It is used to clean up any side effects that were created in the effect. The cleanup function is executed in two cases:

* After the component instance has unmounted, in order to give us the opportunity to reset the side effect that we created, if that's necessary.
* Before the effect is executed again, in order to clean up the results of the previous side effect.

When the cleanup function is executed after the component instance has unmounted, all of the state variables for the component have been destroyed. However, the cleanup function is still able to access the variables that were in scope when the cleanup function was created. This is because the cleanup function is closed over those variables.

**Example**

The following example shows how the closure affects the cleanup function:

```javascript
const MovieDetails = () => {
  const [movie, setMovie] = useState();

  useEffect(() => {
    // Fetch a movie from an API

    // Set the page title
    document.title = movie.title;

    // Return a cleanup function to reset the page title
    return () => {
      // The cleanup function can still access the movie variable, even though it has been destroyed
      document.title = movie.title;
    };
  }, [movie]);

  return (
    <div>
      <h1>{movie?.title}</h1>
    </div>
  );
};
```

In this example, the cleanup function sets the page title back to the title of the movie that was selected before the component was unmounted. This is possible because the cleanup function is closed over the movie variable.

**Conclusion**

The closure is a powerful feature of JavaScript that allows functions to retain access to variables that would otherwise be garbage collected. This can be useful for writing cleanup functions in React.

# One More Effect: Listening to a Keypress

**Detailed notes on handling keypress events in React**

**Overview**

To handle keypress events in React, you can use the `useEffect` hook to listen for the `keydown` event on the document element. When the user presses a key, the `keydown` event will be triggered and the `useEffect` hook callback function will be executed.

To clean up the event listener when the component unmounts, you can return a function from the `useEffect` hook callback function. This function will be executed when the component unmounts and it should remove the event listener from the document element.

**Example**

The following code shows an example of how to handle keypress events in React:

```javascript
import { useEffect, useState } from "react";

const MovieDetails = () => {
  const [movie, setMovie] = useState();

  useEffect(() => {
    // Listen for the keydown event on the document element
    document.addEventListener("keydown", (event) => {
      // If the user presses the Escape key, close the movie
      if (event.code === "Escape") {
        handleCloseMovie();
      }
    });

    // Return a cleanup function to remove the event listener
    return () => {
      document.removeEventListener("keydown", (event) => {
        // If the user presses the Escape key, close the movie
        if (event.code === "Escape") {
          handleCloseMovie();
        }
      });
    };
  }, []);

  return (
    <div>
      <h1>{movie?.title}</h1>
    </div>
  );
};
```

**Why do we need a cleanup function?**

We need a cleanup function because otherwise the event listener will remain attached to the document element even after the component unmounts. This can lead to memory leaks and performance problems.

**When do we need to return a cleanup function?**

You should return a cleanup function from the `useEffect` hook callback function whenever you create a side effect in the effect. A side effect is anything that changes the DOM or interacts with an external API.

In the example above, we are creating a side effect by adding an event listener to the document element. Therefore, we need to return a cleanup function to remove the event listener when the component unmounts.

**Best practices**

Here are some best practices for handling keypress events in React:

* Use the `useEffect` hook to listen for the `keydown` event on the document element.
* Return a cleanup function from the `useEffect` hook callback function to remove the event listener when the component unmounts.
* Be specific about the key codes that you want to listen for. For example, if you only want to listen for the Enter key, then use the `Enter` key code instead of listening for all key codes.
* Avoid using the `preventDefault` method in the event listener. This can prevent other event handlers from being executed.

**Conclusion**

Handling keypress events in React is a simple but important task. By following the best practices outlined above, you can ensure that your code is efficient and reliable.

# 

