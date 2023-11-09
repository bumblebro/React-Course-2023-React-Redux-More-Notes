# How to Split a UI Into Components
**Notes on "Splitting a huge component into many smaller components in React"**

**What is a component?**

A component is a reusable piece of code that renders HTML, CSS, and JavaScript. Components are the building blocks of React applications.

**Why should we split a huge component into many smaller components?**

There are several reasons why we should split a huge component into many smaller components:

* **Reusability:** Smaller components are more reusable than huge components. This means that we can use the same component in multiple places in our application without having to rewrite the code.
* **Maintainability:** Smaller components are easier to maintain than huge components. This is because it is easier to understand and debug smaller components.
* **Performance:** Smaller components can improve the performance of our application. This is because React can render smaller components more quickly than huge components.

**How to split a huge component into many smaller components**

To split a huge component into many smaller components, we can follow these steps:

1. Identify the different pieces of functionality that the huge component is responsible for.
2. Create a new component for each piece of functionality.
3. Extract the code for each piece of functionality from the huge component and place it in the new component.
4. Update the huge component to use the new components.

**Guidelines for splitting components**

Here are some guidelines for splitting components:

* **Create a logical separation of content.** Each component should have a single, well-defined responsibility.
* **Make components reusable.** If a component can be reused, then it should be.
* **Keep components small and simple.** Components should be easy to understand and maintain.
* **Use descriptive component names.** Component names should be descriptive of what the component does.
* **Avoid declaring components inside other components.** This can make the code difficult to understand and maintain.

**Conclusion**

Splitting a huge component into many smaller components can make our React applications more reusable, maintainable, and performant. By following the guidelines above, we can split our components in a way that is both effective and efficient.

**Code example**

Here is a code example of how to split a huge component into many smaller components:

```javascript
// Huge component
const HugeComponent = () => {
  // ...
};

// Smaller components
const HeaderComponent = () => {
  // ...
};

const ContentComponent = () => {
  // ...
};

const FooterComponent = () => {
  // ...
};

// Split huge component into smaller components
const NewHugeComponent = () => {
  return (
    <div>
      <HeaderComponent />
      <ContentComponent />
      <FooterComponent />
    </div>
  );
};
```

In this example, we have split the `HugeComponent` into three smaller components: `HeaderComponent`, `ContentComponent`, and `FooterComponent`. Each of these smaller components has a single, well-defined responsibility. We have also updated the `NewHugeComponent` to use the new components.

# Component Categories
**Notes on "Different component categories in React"**

**Stateless or presentational components**

Stateless components are components that do not have any state. This means that their output is always the same for the same input props. Stateless components are typically used to render UI elements, such as buttons, headers, and images.

Here is an example of a stateless component:

```javascript
const ButtonComponent = ({ text, onClick }) => {
  return (
    <button onClick={onClick}>
      {text}
    </button>
  );
};
```

This component simply renders a button with the specified text and onClick prop. It does not have any state, so its output is always the same for the same input props.

**Stateful components**

Stateful components are components that have state. This means that their output can change depending on their state. Stateful components are typically used to manage user input, data fetching, and other dynamic behavior.

Here is an example of a stateful component:

```javascript
class CounterComponent extends React.Component {
  state = {
    count: 0,
  };

  incrementCount = () => {
    this.setState({
      count: this.state.count + 1,
    });
  };

  render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.incrementCount}>Increment</button>
      </div>
    );
  }
}
```

This component has a state variable called `count`. It also has an `incrementCount()` method that increments the `count` state variable. When the `incrementCount()` method is called, the component's output will change because its state has changed.

**Structural components**

Structural components are components that provide structure to the application, such as pages, layouts, and screens. Structural components are typically composed of smaller components.

Here is an example of a structural component:

```javascript
const AppLayout = () => {
  return (
    <div>
      <Header />
      <Content />
      <Footer />
    </div>
  );
};
```

This component simply composes three smaller components: `Header`, `Content`, and `Footer`. The `AppLayout` component is responsible for providing the structure of the application, but it does not contain any specific UI elements.

**Conclusion**

Stateless, stateful, and structural components are three categories of components that naturally emerge in most React code bases. Each category of component has its own specific purpose and benefits.

Stateless components are typically used to render UI elements. They are simple and efficient, but they cannot manage state.

Stateful components are typically used to manage user input, data fetching, and other dynamic behavior. They are more complex than stateless components, but they are more powerful and flexible.

Structural components are typically used to provide structure to the application. They are composed of smaller components and they are responsible for the overall layout of the application.

# Prop Drilling
Here are some detailed notes from the paragraph given below, with code examples:

## Problem: Not dynamically calculating the number of results

```js
// Before
const NumResults = () => {
  return <span>X</span>;
};
```

The problem is that the number of results is not being dynamically calculated. It is hardcoded to `X`.

## Solution: Lift the state up to the App component and pass it down as a prop

```js
// After
const NumResults = ({ movies }) => {
  return <span>{movies.length}</span>;
};

const App = () => {
  const [movies, setMovies] = useState([]);

  // ...

  return (
    <div>
      <NumResults movies={movies} />
      <MovieList movies={movies} />
    </div>
  );
};
```

The solution is to lift the `movies` state up to the `App` component and pass it down as a prop to the `NumResults` component. This way, the `NumResults` component can dynamically calculate the number of results by reading the `movies` prop.

## Problem: Prop drilling

```js
// After
const MovieList = ({ movies }) => {
  return (
    <ListBox movies={movies}>
      <WatchedBox movies={movies} />
    </ListBox>
  );
};

const ListBox = ({ movies, children }) => {
  return (
    <ul>
      {children}
    </ul>
  );
};

const WatchedBox = ({ movies }) => {
  // ...
};
```

We now have a problem called prop drilling. This means that we are passing the `movies` prop through multiple nested components in order to get it to the `WatchedBox` component, which is deeply nested in the component tree.

## What is prop drilling?

Prop drilling is when we need to pass a prop through several nested child components in order to get that data into some deeply nested component.

## Why is prop drilling a problem?

Prop drilling can be a problem for several reasons:

* It can make the code more difficult to read and maintain.
* It can lead to performance problems, especially if the prop is large or is being passed through a lot of components.
* It can make the code more fragile, as changes to the prop drilling chain can break the application.

## How to avoid prop drilling

There are a few ways to avoid prop drilling:

* **Use context:** Context allows us to share data between components without having to pass it down as props.
* **Use component composition:** Component composition allows us to break down complex components into smaller, more reusable components. This can help to reduce the need for prop drilling.
* **Use a state management library:** A state management library, such as Redux, can help to centralize the state of our application and make it easier to share data between components.

## Conclusion

Prop drilling is a problem that can occur when we need to pass a prop through several nested components in order to get it to some deeply nested component. There are a few ways to avoid prop drilling, such as using context, component composition, or a state management library.

# Fixing Prop Drilling With Composition (And Building a Layout)

**Component Composition in React to Fix Prop Drilling**

**Problem:**

Prop drilling is when we have to pass a prop down through multiple levels of components in order to reach the component that actually needs it. This can make our code difficult to read and maintain.

**Solution:**

Component composition is a way to solve the prop drilling problem. It involves breaking down our UI into smaller components and passing those components to other components as props. This way, we can avoid having to pass props down through multiple levels of components.

**Example:**

```jsx
// Before
const App = () => {
  const movies = []; // Get movies from API

  return (
    <div>
      <NavBar movies={movies} />
      <Main movies={movies} />
    </div>
  );
};

const NavBar = ({ movies }) => {
  return (
    <div>
      <Search />
      <NumResults movies={movies} />
    </div>
  );
};

const Main = ({ movies }) => {
  return (
    <div>
      <ListBox movies={movies} />
      <WatchedBox movies={movies} />
    </div>
  );
};
```

In the above example, we have to pass the `movies` prop down to the `NumResults` component through the `NavBar` component. This is prop drilling.

**Using component composition, we can rewrite the above code as follows:**

```jsx
// After
const App = () => {
  const movies = []; // Get movies from API

  return (
    <div>
      <NavBar children={<NumResults movies={movies} />} />
      <Main children={<ListBox movies={movies} />} />
    </div>
  );
};

const NavBar = ({ children }) => {
  return (
    <div>
      <Search />
      {children}
    </div>
  );
};

const Main = ({ children }) => {
  return (
    <div>
      {children}
    </div>
  );
};

const ListBox = ({ movies }) => {
  return (
    <div>
      {movies.map((movie) => <div key={movie.id}>{movie.title}</div>)}
    </div>
  );
};
```

In the above code, we are now passing the `NumResults` component as a prop to the `NavBar` component. This means that we no longer have to pass the `movies` prop down to the `NumResults` component.

**Benefits of component composition:**

* It makes our code easier to read and maintain.
* It makes our code more reusable.
* It makes our code more modular.

**Conclusion:**

Component composition is a powerful technique that can help us to write better React code. It can help us to avoid prop drilling, make our code more reusable, and make our code more modular.
# Using Composition to Make a Reusable Box

**Creating a Reusable Box Component with React Composition**

**Problem:**

We have two components, `WatchedBox` and `ListBox`, that are very similar. They both have the same state, class name, and button. The only difference is that they render different children conditionally.

**Solution:**

We can create a reusable `Box` component that both `WatchedBox` and `ListBox` can use. This will allow us to avoid repeating the same code and make our application more modular.

**Steps:**

1. Create a new component called `Box`.
2. Move the state, class name, and button logic from the `WatchedBox` and `ListBox` components to the `Box` component.
3. Add a `children` prop to the `Box` component. This will allow us to pass in the different content that we want to render inside the box.
4. Update the `WatchedBox` and `ListBox` components to use the `Box` component. Simply pass in the content that you want to render as the `children` prop.

**Example:**

```jsx
// Before

const WatchedBox = () => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="box">
      {isOpen && <WatchedList />}
      <button onClick={() => setIsOpen(!isOpen)}>Toggle</button>
    </div>
  );
};

const ListBox = () => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="box">
      {isOpen && <MovieList />}
      <button onClick={() => setIsOpen(!isOpen)}>Toggle</button>
    </div>
  );
};
```

```jsx
// After

const Box = ({ children }) => {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div className="box">
      {isOpen && children}
      <button onClick={() => setIsOpen(!isOpen)}>Toggle</button>
    </div>
  );
};

const WatchedBox = () => {
  return <Box children={<WatchedList />} />;
};

const ListBox = () => {
  return <Box children={<MovieList />} />;
};
```

**Benefits:**

* Reduced code duplication
* Increased modularity
* More reusable code

**Conclusion:**

Component composition is a powerful technique that can be used to create reusable components, solve prop drilling, and build better layouts. By using component composition, we can write more efficient and maintainable code.

#  Passing Elements as Props (Alternative to children)

**Using an Explicit Prop Instead of the Children Prop for Component Composition**

**Problem:**

We want to use component composition to build our React application, but we want to avoid using the `children` prop.

**Solution:**

We can use an explicit prop instead of the `children` prop for component composition. This means that we will explicitly define the prop and pass in the component that we want to render as the value of the prop.

**Steps:**

1. Define an explicit prop in the parent component.
2. Pass the component that you want to render as the value of the prop.
3. In the child component, accept the prop and render it.

**Example:**

```jsx
// Parent component

const ParentComponent = () => {
  const [element, setElement] = useState(<MovieList />);

  return (
    <div>
      <Box element={element} />
    </div>
  );
};

// Child component

const Box = ({ element }) => {
  return (
    <div className="box">
      {element}
    </div>
  );
};
```

**Benefits:**

* Can be used to pass in multiple elements with separate names
* Can be used to avoid the implicit nature of the `children` prop

**Conclusion:**

Using an explicit prop instead of the `children` prop for component composition is a viable option, but it is not the preferred way to do things in React. The `children` prop is a special prop that is designed for component composition, and it is the preferred way to pass components to other components.

# Handling Hover Events

**Handling Hover Events to Display Temporary Rating**

**Problem:**

We want to display a temporary rating whenever a user hovers over the stars.

**Solution:**

We can use the `onMouseEnter` and `onMouseLeave` events to handle hover events. We will also need to create a new state variable to store the temporary rating.

**Steps:**

1. Create a new state variable to store the temporary rating.
2. Add `onMouseEnter` and `onMouseLeave` event handlers to the star component.
3. Update the state variable in the event handlers.
4. Display the temporary rating in the UI.

**Example:**

```jsx
// State
const [rating, setRating] = useState(0);
const [tempRating, setTempRating] = useState(0);

// Event handlers
const onHoverIn = (rating) => {
  setTempRating(rating);
};

const onHoverOut = () => {
  setTempRating(0);
};

// Render
return (
  <div>
    <Star
      rating={rating}
      onHoverIn={onHoverIn}
      onHoverOut={onHoverOut}
    />

    <div>{tempRating}</div>
  </div>
);
```

**Conclusion:**

By handling hover events and using a state variable to store the temporary rating, we can easily display a temporary rating whenever a user hovers over the stars.
# Props as a Component API
**Thinking About Props for Reusable Components**

**Problem:**

When building reusable components, it is important to carefully consider the props that the component needs. The props should be the public API of the component, and should allow consumers to interact with the component without exposing too much complexity.

**Solution:**

To strike the right balance between too few and too many props, consider the following:

* What functionality does the component need to provide?
* What configuration options do consumers need?
* How complex is the component's internal logic?

If the component is simple, a few well-chosen props may be sufficient. If the component is more complex, consider providing default values for many of the props to make it easier for consumers to use.

**Steps:**

**1. Identify the component's functionality.** What does the component do? What data does it need to operate? What actions can it perform?

**2. Consider the needs of consumers.** What configuration options do consumers need? What information will they need to provide to the component? What should the component's public interface look like?

**3. Strike a balance between flexibility and simplicity.** Avoid exposing too much complexity to consumers, but make sure that the component is flexible enough to meet their needs.

**Example:**

```jsx
// Simple weather component with one prop: location

function Weather({ location }) {
  // Fetch the weather data for the given location
  const weatherData = fetchWeatherData(location);

  // Display the weather data
  return (
    <div>
      <h1>Weather for {location}</h1>
      <p>{weatherData.temperature} degrees Celsius</p>
    </div>
  );
}
```

```jsx
// More complex weather component with multiple props

function Weather({
  location,
  days,
  hourly,
  temperatureUnit,
  dataToDisplay,
}) {
  // Fetch the weather data for the given location, days, and hourly option
  const weatherData = fetchWeatherData(location, days, hourly);

  // Display the weather data according to the temperatureUnit and dataToDisplay props
  return (
    <div>
      <h1>Weather for {location}</h1>
      <p>{weatherData.temperature} {temperatureUnit}</p>
      <ul>
        {dataToDisplay.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>
  );
}
```

**Conclusion:**

By carefully considering the component's functionality, the needs of consumers, and the balance between flexibility and simplicity, you can design props that make your reusable components easy to use and maintain.

# Improving Reusability With Props

**Making the Rating Component More Flexible and Reusable**

**Problem:**

The rating component is currently not very flexible or reusable. It does not allow consumers to specify the colors, sizes, or font style of the stars or text. It also does not allow consumers to display a message instead of the rating number, or to set a default rating.

**Solution:**

We can make the rating component more flexible and reusable by adding props that allow consumers to specify the following:

* Colors
* Sizes
* Font style
* Message array
* Default rating

**Steps:**

1. Add props for colors, sizes, and font style.
2. Update the component to use the prop values instead of the default values.
3. Add a prop for a message array.
4. Update the component to display the message array instead of the rating number if the message array is provided.
5. Add a prop for a default rating.
6. Update the component to initialize the rating state with the default rating prop if it is provided.

**Example:**

```jsx
const Rating = ({
  rating,
  color,
  size,
  messages,
  defaultRating,
}) => {
  const [stateRating, setStateRating] = useState(defaultRating || 0);

  const handleRate = (newRating) => {
    setStateRating(newRating);
  };

  const renderStars = () => {
    const stars = [];

    for (let i = 0; i < rating; i++) {
      stars.push(
        <Star
          key={i}
          color={color}
          size={size}
          onClick={() => handleRate(i + 1)}
        />
      );
    }

    return stars;
  };

  return (
    <div className="rating">
      <div className="stars">{renderStars()}</div>
      {messages && messages.length === rating && (
        <div className="message">{messages[rating - 1]}</div>
      )}
    </div>
  );
};
```

**Usage:**

```jsx
<Rating
  rating={3}
  color="red"
  size="48"
  messages={[
    "Terrible",
    "Bad",
    "Okay",
    "Good",
    "Amazing",
  ]}
  defaultRating={2}
/>
```

This will render a rating component with red stars that are 48 pixels in size. The component will also display the message "Good" because the rating is 3 and the messages array has 5 elements.

**Conclusion:**

By adding props to the rating component, we have made it more flexible and reusable. Consumers can now specify the colors, sizes, font style, message array, and default rating of the component. This makes it easier for consumers to use the component in their own applications.

# PropTypes

**Adding Type Checking to the Rating Component Using Proptypes**

**Problem:**

The rating component does not currently have type checking enabled for its props. This means that consumers of the component can pass in any type of data for the props, even if it is not the type that the component expects. This can lead to bugs and unexpected behavior.

**Solution:**

We can add type checking to the rating component using the `proptypes` package. This package provides a number of validators that we can use to check the type of each prop.

**Steps:**

1. Import the `proptypes` package.
2. Add a `proptypes` property to the rating component.
3. For each prop, specify the expected type using a proptypes validator.

**Example:**

```jsx
// Import the proptypes package.
import PropTypes from 'prop-types';

// Add type checking to the rating component.
const Rating = ({
  rating,
  color,
  size,
  messages,
  defaultRating,
  onSetRating,
}) => {
  ...

  // proptypes
  Rating.propTypes = {
    rating: PropTypes.number.isRequired,
    color: PropTypes.string,
    size: PropTypes.number,
    messages: PropTypes.array,
    defaultRating: PropTypes.number,
    onSetRating: PropTypes.func.isRequired,
  };
};
```

**Benefits:**

Adding type checking to the rating component has a number of benefits:

* It helps to prevent bugs and unexpected behavior.
* It makes the component more reliable and easier to use for consumers.
* It documents the expected types of each prop, which makes the code more readable and maintainable.

**Notes:**

* Proptypes is a built-in React package, but it is not required.
* If you are using TypeScript, you can use TypeScript's type system to type check your component's props instead of proptypes.
* It is generally not recommended to mark props as required unless they are absolutely necessary. Instead, it is better to provide default values for all props.

**Conclusion:**

Adding type checking to the rating component is a simple and effective way to improve the quality and reliability of the code.

