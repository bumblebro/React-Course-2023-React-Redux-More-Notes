# Introduction to Redux

Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Understand the concept of Redux and its mechanics, including the differences between Redux and the useReducer hook.

**Problem:**

Redux can seem complex and confusing due to its additional components and concepts compared to the useReducer hook.

**Solution:**

- Break down the Redux cycle into smaller steps to understand the flow of state updates.
- Compare Redux components to their counterparts in the useReducer hook to grasp the similarities and differences.
- Use an analogy to visualize the interaction between components in Redux.

**Key Points:**

- Redux is a state management library for global UI state that needs frequent updates.
- Redux actions are dispatched to the store, not directly to the reducer.
- The store is a centralized container for global state and holds one or more reducers.
- Action creators are functions that automate the creation of action objects.
- Redux follows a similar cycle to useReducer, but with additional components.

**Code:**

```javascript
// Action creator example
function depositMoney(amount) {
  return {
    type: 'DEPOSIT_MONEY',
    payload: amount,
  };
}
```

**Analogy:**

- Action creator: The person who gives instructions to the bank teller.
- Action: The instructions themselves.
- Dispatcher: The bank teller who updates the bank vault.
- Store: The bank vault that holds the money.
- Reducer: The process of updating the money in the bank vault based on the instructions.

**Additional Notes:**

- Redux is not always necessary for global state management, especially when dealing with remote state.
- Redux's complexity arises from its separation of concerns and its centralized state management approach.
- Understanding the useReducer hook provides a solid foundation for learning Redux.

# Creating a Reducer: Bank Account
Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Establish a basic understanding of Redux by implementing a reducer function without React integration.

**Problem:**

Redux can appear complex due to its additional components and concepts compared to the useReducer hook.

**Solution:**

- Create a reducer function that handles actions for depositing, withdrawing, requesting a loan, and paying back a loan.
- Use a switch statement to select the appropriate action type and update the state accordingly.
- Return the updated state from the reducer function.

**Key Points:**

- Redux reducers are pure functions that calculate the new state based on the current state and the action.
- Action types should be written in the shape of the state domain and the event name.
- Reducers should return the original state if they receive an unknown action type.

**Code:**

```javascript
const initialState = {
  balance: 0,
  loan: 0,
  loanPurpose: '',
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'account.deposit':
      return {
        ...state,
        balance: state.balance + action.payload,
      };
    case 'account.withdraw':
      return {
        ...state,
        balance: state.balance - action.payload,
      };
    case 'account.requestLoan':
      if (state.loan > 0) {
        return state;
      }
      return {
        ...state,
        loan: action.payload.amount,
        loanPurpose: action.payload.purpose,
      };
    case 'account.payLoanBack':
      return {
        ...state,
        loan: 0,
        loanPurpose: '',
        balance: state.balance - action.payload,
      };
    default:
      return state;
  }
}
```

**Additional Notes:**

- The reducer function is not yet integrated with React, but it serves as the foundation for managing the bank account state.
- The action types follow the recommended format of "stateDomain.eventName".
- The reducer handles unknown action types by returning the original state, preventing errors.
- The next lecture will focus on creating the Redux store and integrating it with the reducer.


# Creating a Redux Store

Sure, here are detailed notes with code from the paragraph given below:

**Objective:**

Set up the Redux store and demonstrate basic state updates using dispatching actions.

**Problem:**

Redux introduces additional components and concepts compared to the useReducer hook, requiring a deeper understanding of its mechanics.

**Solution:**

- Install the Redux package using npm.
- Create a store using the createStore method from Redux.
- Dispatch actions to the store to modify the state.
- Use console.log to observe the state changes in the console.
- Introduce action creators to automate action creation.

**Key Points:**

- The Redux store is a centralized container for global state.
- Dispatching actions is the primary way to update state in Redux.
- Action creators simplify action creation by encapsulating the action type and payload.

**Code:**

```javascript
import { createStore } from 'redux';
import reducer from './store';

const store = createStore(reducer);

// Dispatching actions to update state
store.dispatch({ type: 'account.deposit', payload: 500 });
console.log('State after deposit:', store.getState());

store.dispatch({ type: 'account.withdraw', payload: 200 });
console.log('State after withdraw:', store.getState());

// Action creator for requesting a loan
const requestLoan = (amount, purpose) => ({
  type: 'account.requestLoan',
  payload: {
    amount,
    purpose,
  },
});

store.dispatch(requestLoan(1000, 'Buy a car'));
console.log('State after loan request:', store.getState());

// Action creator for paying back a loan
const payLoanBack = () => ({
  type: 'account.payLoanBack',
});

store.dispatch(payLoanBack());
console.log('State after paying back loan:', store.getState());
```

**Additional Notes:**

- The provided code demonstrates basic state updates using Redux actions.
- Action creators can be defined in separate files for better organization.
- Redux provides a more structured approach to global state management compared to the useReducer hook.
- Understanding Redux concepts is essential for integrating it with React applications.

# Working With Action Creators

Sure, here are the detailed notes with code from the paragraph given below:

### Creating Action Creators

Action creators are functions that return actions. They are a useful convention that Redux developers have used for a long time. Although Redux would work without action creators, they make the code more reusable and less prone to typos.

Here is an example of how to create action creators for depositing and withdrawing money from a bank account:

```javascript
function deposit(amount) {
  return {
    type: 'ACCOUNT_DEPOSIT',
    amount: amount
  };
}

function withdraw(amount) {
  return {
    type: 'ACCOUNT_WITHDRAW',
    amount: amount
  };
}
```

These action creators can then be used to dispatch actions to the store:

```javascript
store.dispatch(deposit(100));
store.dispatch(withdraw(50));
```

Here is an example of how to create an action creator for requesting a loan:

```javascript
function requestLoan(amount, purpose) {
  return {
    type: 'ACCOUNT_REQUEST_LOAN',
    amount: amount,
    purpose: purpose
  };
}
```

This action creator can then be used to dispatch an action to the store:

```javascript
store.dispatch(requestLoan(1000, 'Buy a cheap car.'));
```

Here is an example of how to create an action creator for paying off a loan:

```javascript
function payLoan() {
  return {
    type: 'ACCOUNT_PAY_LOAN'
  };
}
```

This action creator can then be used to dispatch an action to the store:

```javascript
store.dispatch(payLoan());
```

In older React codebases, it was common to place the action type strings into separate variables. However, this is no longer considered to be best practice, and it is better to just include the action type strings directly in the action creators.

# Adding More State: Customer

Sure, here are the detailed notes with code from the paragraph given below:

### Creating Action Creators and Reducers for Customer State

After creating action creators for account transactions, let's move on to creating action creators and reducers for customer state.

**Initial State**

```javascript
const initialStateCustomer = {
  fullName: '',
  nationalID: '',
  createdAt: '',
};
```

**Action Creators**

```javascript
function createCustomer(fullName, nationalID) {
  return {
    type: 'CUSTOMER_CREATE',
    payload: {
      fullName,
      nationalID,
      createdAt: new Date().toISOString(),
    },
  };
}

function updateName(fullName) {
  return {
    type: 'CUSTOMER_UPDATE_NAME',
    payload: {
      fullName,
    },
  };
}
```

**Reducer**

```javascript
function customerReducer(state = initialStateCustomer, action) {
  switch (action.type) {
    case 'CUSTOMER_CREATE':
      return {
        ...state,
        fullName: action.payload.fullName,
        nationalID: action.payload.nationalID,
        createdAt: action.payload.createdAt,
      };
    case 'CUSTOMER_UPDATE_NAME':
      return {
        ...state,
        fullName: action.payload.fullName,
      };
    default:
      return state;
  }
}
```

**Combining Reducers**

```javascript
import { combineReducers } from 'redux';
import accountReducer from './accountReducer';
import customerReducer from './customerReducer';

const rootReducer = combineReducers({
  account: accountReducer,
  customer: customerReducer,
});

export default rootReducer;
```

**Using Action Creators**

```javascript
store.dispatch(createCustomer('John Doe', '1234567890'));
store.dispatch(updateName('Jane Doe'));
```

**Accessing Customer State**

```javascript
console.log(store.getState().customer);
```

# Professional Redux File Structure: State Slices

Sure, here are the detailed notes with code from the paragraph given below:

### Organizing Code into Slices

Redux developers used to create separate folders for reducers and action creators. However, this approach leads to jumping around between files. Instead, it is recommended to organize the code into slices, where each slice contains the initial state, reducer, and action creators for a specific part of the state.

**Creating Slices**

1. Create a `features` folder to hold all the slices.
2. Create a folder for each feature (e.g., `account`, `customer`).
3. Inside each feature folder, create an `index.js` file to export the slice.
4. In each `index.js` file, import the initial state, reducer, and action creators for the feature.
5. Export the reducer as a default export and the action creators as named exports.

**Example Slices**

**account/index.js**

```javascript
import { initialStateAccount } from './initialStateAccount';
import accountReducer from './accountReducer';
import { deposit, withdraw, requestLoan, payLoan } from './actionCreators';

export default accountReducer;
export { deposit, withdraw, requestLoan, payLoan };
```

**customer/index.js**

```javascript
import { initialStateCustomer } from './initialStateCustomer';
import customerReducer from './customerReducer';
import { createCustomer, updateName } from './actionCreators';

export default customerReducer;
export { createCustomer, updateName };
```

**Combining Reducers**

```javascript
import { combineReducers } from 'redux';
import accountReducer from './features/account/index';
import customerReducer from './features/customer/index';

const rootReducer = combineReducers({
  account: accountReducer,
  customer: customerReducer,
});

export default rootReducer;
```

**Benefits of Slices**

- Improves code readability and maintainability
- Reduces the need to jump between files
- Promotes separation of concerns

**Next Steps**

1. Inject the store into the React application.
2. Connect React components to the store.

# Back to React! Connecting our Redux App With React

**Connecting Redux Store with React Application**

**Prerequisites:**

- Redux and React Redux packages are installed.
- A Redux store has been created.

**Steps:**

1. **Import the Provider from React Redux.**

```javascript
import React from 'react';
import { Provider } from 'react-redux';
import { store } from './store'; // Replace './store' with the actual path to your store

**2. Wrap your entire application in the Provider.**

```javascript
const App = () => {
  return (
    <Provider store={store}>
      {/* Your application components */}
    </Provider>
  );
};
```

**3. Read data from the Redux store using the useSelector hook.**

```javascript
import React from 'react';
import { useSelector } from 'react-redux';

const Customer = () => {
  const customer = useSelector(state => state.customer); // Replace 'customer' with the actual name of the property in your store state
  const fullName = customer.firstName + ' ' + customer.lastName;

  return (
    <div>
      Welcome, {fullName}!
    </div>
  );
};


**Explanation:**

- The Provider component makes the Redux store available to all child components.
- The useSelector hook takes a callback function that receives the entire Redux store state.
- The callback function can extract any data from the store state and return it.
- The component will re-render whenever the store state changes, ensuring that the data is always up-to-date.


# Dispatching Actions from Our React App

**Dispatching Actions to Redux Store from React Components**

**Prerequisites:**

- Redux and React Redux packages are installed.
- A Redux store has been created.
- Action creators are defined in Redux slices.

**Steps:**

1. **Import the useDispatch hook from React Redux.**

```javascript
import React from 'react';
import { useDispatch } from 'react-redux';
```

2. **Inside a React component, use the useDispatch hook to get the dispatch function.**

```javascript
const CreateCustomer = () => {
  const dispatch = useDispatch();
  ...
};
```

3. **Call the dispatch function with the action creator function and any necessary arguments.**

```javascript
const handleClick = () => {
  const fullName = firstName + ' ' + lastName;
  const nationalID = idNumber;

  if (!fullName || !nationalID) {
    return;
  }

  dispatch(createCustomer({ fullName, nationalID }));
};
```

**Explanation:**

- The useDispatch hook provides a way to access the Redux store's dispatch function directly from within a React component.
- The dispatch function is used to trigger actions, which are objects that signal a change to the Redux store.
- The action creator function returns the action object that will be dispatched.

**Example:**

```javascript
// action creator in customerSlice.js
export const createCustomer = (customer) => ({
  type: 'CREATE_CUSTOMER',
  payload: customer,
});

// component dispatching an action
const CreateCustomer = () => {
  const dispatch = useDispatch();

  const handleClick = () => {
    const fullName = firstName + ' ' + lastName;
    const nationalID = idNumber;

    if (!fullName || !nationalID) {
      return;
    }

    dispatch(createCustomer({ fullName, nationalID }));
  };

  return (
    <div>
      <input type="text" placeholder="First Name" />
      <input type="text" placeholder="Last Name" />
      <input type="text" placeholder="National ID" />
      <button onClick={handleClick}>Create Customer</button>
    </div>
  );
};
```

In this example, the CreateCustomer component dispatches the CREATE_CUSTOMER action when the user clicks the "Create Customer" button. The action creator provides the necessary information to create a new customer in the Redux store.

# The Legacy Way of Connecting Components to Redux

**Connecting React Components to Redux Store with Connect API**

**Prerequisites:**

- Redux and React Redux packages are installed.
- A Redux store has been created.

**Steps:**

1. **Import the connect function from React Redux.**

```javascript
import React from 'react';
import { connect } from 'react-redux';
```

2. **Create a mapStateToProps function that takes the Redux store state as an argument and returns an object with the props that the component needs.**

```javascript
const mapStateToProps = (state) => ({
  balance: state.account.balance,
});
```

3. **Pass the mapStateToProps function to the connect function and the component you want to connect.**

```javascript
const BalanceDisplay = (props) => {
  const { balance } = props;

  return (
    <div>
      Balance: ${formatCurrency(balance)}
    </div>
  );
};

export default connect(mapStateToProps)(BalanceDisplay);
```

**Explanation:**

- The connect API is a higher-order component that wraps the component you want to connect and injects the props that the component needs.
- The mapStateToProps function is used to select the parts of the Redux store state that the component needs.
- The connect function returns a new component that is wrapped by the connect higher-order component.

**Example:**

```javascript
// component without connect API
const BalanceDisplay = (props) => {
  // props.balance will always be undefined
  const { balance } = props;

  return (
    <div>
      Balance: ${formatCurrency(balance)}
    </div>
  );
};

// connecting the component using connect API
const BalanceDisplayConnected = connect(mapStateToProps)(BalanceDisplay);
```

In this example, the BalanceDisplay component is connected to the Redux store using the connect API. The mapStateToProps function extracts the balance property from the Redux store state and passes it to the BalanceDisplay component as a prop. The BalanceDisplayConnected component is the new component that is wrapped by the connect higher-order component.
 
# Redux Middleware and Thunks

**Understanding Redux Middleware**

**What is Middleware?**

Middleware is a function that sits between dispatching an action and the store in Redux. It allows developers to run some code after dispatching an action, but before that action reaches the reducer in the store. This makes it a perfect place to handle asynchronous operations, such as making API calls.

**Why use Middleware?**

There are several reasons why you might want to use middleware in your Redux application:

* **Handle asynchronous operations:** Middleware allows you to make asynchronous API calls or perform other time-consuming tasks without blocking the main thread.
* **Implement side effects:** Middleware can be used to log actions to the console, set timers, or even pause or cancel actions altogether.
* **Encapsulate logic:** Middleware can be used to encapsulate complex logic away from components and reducers.

**How does Middleware work?**

When an action is dispatched, it is first passed to the middleware chain. Each middleware in the chain has the opportunity to intercept the action and perform some custom logic. If the middleware does not modify the action, it passes it on to the next middleware in the chain. Once the action reaches the end of the middleware chain, it is finally dispatched to the store.

**Redux Thunk**

Redux Thunk is a popular middleware that allows you to handle asynchronous operations in your Redux application. It provides a way to dispatch functions instead of plain objects, and these functions can perform asynchronous operations and then dispatch actions with the results.

**Example:**

```javascript
const fetchUserData = (userId) => {
  return (dispatch) => {
    fetch(`https://api.example.com/users/${userId}`)
      .then(response => response.json())
      .then(userData => {
        dispatch({
          type: 'FETCH_USER_DATA',
          payload: userData
        });
      });
  };
};
```

In this example, the fetchUserData function is a thunk action creator. It returns a function that dispatches a FETCH_USER_DATA action with the user data once it is fetched from the API.

**Implementing Middleware in your application**

To use middleware in your Redux application, you will need to install a middleware package, such as Redux Thunk. Then, you will need to configure the middleware chain in your store creation process. For example, to use Redux Thunk, you would do the following:

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import reducer from './reducer';

const store = createStore(reducer, applyMiddleware(thunk));
```

Once you have configured the middleware chain, you can use thunk action creators to dispatch asynchronous actions.

# Making an API Call With Redux Thunks

Sure, here are detailed notes with code from the paragraph given below:

**How to Use Redux Thunks to Implement a Feature Where the User Can Deposit Money into the Account in a Foreign Currency**

**Step 1: Install the Redux Thunk Middleware**

```bash
npm install redux-thunk
```

**Step 2: Apply the Redux Thunk Middleware to the Store**

```javascript
import thunk from 'redux-thunk';

const store = createStore(reducer, applyMiddleware(thunk));
```

**Step 3: Use the Redux Thunk Middleware in Action Creator Functions**

```javascript
import thunk from 'redux-thunk';

export const depositMoney = (amount, currency) => {
  if (currency === 'USD') {
    return {
      type: 'ACCOUNT_DEPOSIT',
      payload: {
        amount
      }
    };
  } else {
    return async (dispatch, getState) => {
      const response = await fetch('https://frankfurter.app/latest?from=' + currency + '&to=USD');
      const data = await response.json();
      const convertedAmount = amount * data.rates.USD;

      dispatch({
        type: 'ACCOUNT_DEPOSIT',
        payload: {
          amount: convertedAmount
        }
      });
    };
  }
};
```

**Step 4: Dispatch the Action with the Currency**

```javascript
store.dispatch(depositMoney(100, 'EUR'));
```

**Step 5: Add a Loading Indicator**

```javascript
const initialState = {
  amount: 0,
  isLoading: false
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ACCOUNT_DEPOSIT':
      return {
        ...state,
        amount: action.payload.amount
      };
    case 'ACCOUNT_CONVERTING_CURRENCY':
      return {
        ...state,
        isLoading: true
      };
    case 'ACCOUNT_CONVERSION_COMPLETE':
      return {
        ...state,
        isLoading: false
      };
    default:
      return state;
  }
};

export const depositMoney = (amount, currency) => {
  if (currency === 'USD') {
    return {
      type: 'ACCOUNT_DEPOSIT',
      payload: {
        amount
      }
    };
  } else {
    return async (dispatch, getState) => {
      dispatch({
        type: 'ACCOUNT_CONVERTING_CURRENCY'
      });

      const response = await fetch('https://frankfurter.app/latest?from=' + currency + '&to=USD');
      const data = await response.json();
      const convertedAmount = amount * data.rates.USD;

      dispatch({
        type: 'ACCOUNT_CONVERSION_COMPLETE'
      });

      dispatch({
        type: 'ACCOUNT_DEPOSIT',
        payload: {
          amount: convertedAmount
        }
      });
    };
  }
};
```

**Step 6: Disable the Button When Loading**

```javascript
<button disabled={isLoading}>Deposit Money</button>
```

**Step 7: Show a Loading Indicator**

```javascript
{ isLoading ? 'Loading...' : 'Deposit Money' }
```

**Step 8: Dispatch an Action to Reset the Loading Indicator**

```javascript
return {
  ...state,
  isLoading: false
};
```

This code will implement a feature where the user can deposit money into the account in a foreign currency, which will then be converted by calling an external API. The user will be able to see a loading indicator while the conversion is in progress, and the button will be disabled while the conversion is taking place.

# The Redux DevTools

Sure, here are detailed notes with code from the paragraph given below:

**Installing and Using the Redux Dev Tools**

**Step 1: Install the Google Chrome Extension**

1. Open the Chrome Web Store and search for "Redux DevTools".
2. Click on the "Redux DevTools" extension and click "Add to Chrome".
3. Wait for the extension to install.

**Step 2: Install the NPM Package**

1. Open a terminal window and navigate to your project directory.
2. Run the following command:

```bash
npm install redux-devtools-extension
```

**Step 3: Wrap the Apply Middleware Function in ComposeWithDevTools**

1. Open your Redux store configuration file.
2. Import the `composeWithDevTools` function from the `redux-devtools-extension` package.
3. Wrap the `applyMiddleware` function in the `composeWithDevTools` function.

```javascript
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';

const store = createStore(reducer, composeWithDevTools(applyMiddleware(thunk)));
```

**Exploring the Redux Dev Tools**

1. Click on the "Redux" tab in the Chrome Developer Tools.
2. You should see a list of all the actions that have been dispatched to your Redux store.
3. You can click on an action to see its details, including the action type, payload, and the resulting state.
4. You can use the slider at the bottom of the screen to jump back in time to previous states.
5. You can manually dispatch actions by typing the action type and payload into the input field at the bottom of the screen.

**Using the Redux Dev Tools to Debug a Bug**

1. In the Redux Dev Tools, notice that the `account/convertingCurrency` action is being dispatched even when the currency is US dollars.
2. Use the Chrome Developer Tools to find the code that is dispatching the action.
3. Fix the bug by resetting the currency to `USD` after the deposit is made.

**Conclusion**

The Redux Dev Tools are a powerful tool for debugging Redux applications. They allow you to see all the actions that have been dispatched to your store, and to jump back in time to previous states. You can also use them to manually dispatch actions.

# What is Redux Toolkit (RTK)?

Sure, here are detailed notes with code from the paragraph given below:

**Redux Toolkit: The Modern Way of Writing Redux**

**What is Redux Toolkit?**

Redux Toolkit is an opinionated approach to writing Redux code that encourages the use of best practices. It simplifies Redux development by providing a number of pre-built utilities and configurations, including:

* **Automatic action creators:** Redux Toolkit can automatically generate action creators from reducer functions. This reduces boilerplate code and makes it easier to create actions.
* **Immutable state updates:** Redux Toolkit uses the Immer library to make it easier to write immutable state updates. Immer allows you to write code as if you were mutating state directly, but it automatically converts your mutations to non-mutating updates behind the scenes.
* **Middleware setup:** Redux Toolkit automatically sets up Thunk middleware and the Redux DevTools extension. This saves you from having to manually configure these tools.

**Advantages of Redux Toolkit**

* **Reduced boilerplate code:** Redux Toolkit simplifies Redux development by providing a number of pre-built utilities and configurations. This can save you a lot of time and effort, especially when working on large applications.
* **Easier to write immutable state updates:** Immer makes it easier to write immutable state updates by allowing you to write code as if you were mutating state directly. This can make your code more readable and easier to understand.
* **Out-of-the-box middleware and developer tools:** Redux Toolkit automatically sets up Thunk middleware and the Redux DevTools extension. This saves you from having to manually configure these tools, which can be a bit error-prone.

**Compatibility with Classic Redux**

Redux Toolkit is 100% compatible with classic Redux. This means that you can use classic Redux in one part of your application and Redux Toolkit in another part. This can be useful if you're migrating an existing Redux application to Redux Toolkit, or if you need to use a specific feature of classic Redux that isn't available in Redux Toolkit.

**Conclusion**

Redux Toolkit is a powerful tool that can make Redux development easier and more enjoyable. It's worth considering if you're working on a Redux application, or if you're learning Redux for the first time.

**Additional Notes**

* Redux Toolkit is still under active development, so there may be some breaking changes in the future. It's a good idea to keep up with the latest releases and documentation.
* Redux Toolkit is not a replacement for Redux. It's still important to understand the fundamentals of Redux before using Redux Toolkit.

# Creating the Store With RTK

Sure, here are detailed notes with code from the paragraph given below:

**Converting the Store to Redux Toolkit**

**Step 1: Install Redux Toolkit**

1. Open a terminal window and navigate to your project directory.
2. Run the following command:

```bash
npm install @reduxjs/toolkit
```

**Step 2: Import configureStore**

1. Open your Redux store configuration file.
2. Import the `configureStore` function from the `@reduxjs/toolkit` package.

```javascript
import { configureStore } from '@reduxjs/toolkit';
```

**Step 3: Use configureStore to Create the Store**

1. Call the `configureStore` function and pass it an object of options.
2. The `reducer` property should specify an object of reducers.
3. The `middleware` property can be used to specify middleware to be used by the store.

```javascript
const store = configureStore({
  reducer: {
    account: accountReducer,
    customer: customerReducer
  }
});
```

**Step 4: Export the Store**

1. Export the store from the store configuration file.

```javascript
export default store;
```

**Conclusion**

Redux Toolkit can simplify the process of setting up a Redux store. It automatically combines reducers, adds middleware, and sets up the Redux DevTools extension. This can save you a lot of time and effort, especially when working on large applications.

**Additional Notes**

* You can still use the `createStore` function from the classic Redux package if you prefer. However, it is recommended to use `configureStore` from Redux Toolkit instead.
* You can still use the Thunk middleware with Redux Toolkit. It is automatically added to the store by default.
* You can still use the Redux DevTools extension with Redux Toolkit. It is automatically set up by default.

# Creating the Account Slice


Sure, here are detailed notes with code from the paragraph given below:

**Converting the Account State Slice to Redux Toolkit**

**Step 1: Install createSlice**

1. Open a terminal window and navigate to your project directory.
2. Run the following command:

```bash
npm install @reduxjs/toolkit
```

**Step 2: Import createSlice**

1. Open your account state slice file.
2. Import the `createSlice` function from the `@reduxjs/toolkit` package.

```javascript
import { createSlice } from '@reduxjs/toolkit';
```

**Step 3: Create the Slice**

1. Call the `createSlice` function and pass it an object of options.
2. The `name` property should specify the name of the slice.
3. The `initialState` property should specify the initial state of the slice.
4. The `reducers` property should specify an object of reducers.

```javascript
const accountSlice = createSlice({
  name: 'account',
  initialState: {
    balance: 0,
    loan: 0,
    loanPurpose: '',
  },
  reducers: {
    deposit: (state, action) => {
      state.balance += action.payload;
    },
    withdraw: (state, action) => {
      state.balance -= action.payload;
    },
    requestLoan: (state, action) => {
      if (state.loan === 0) {
        state.loan = action.payload.amount;
        state.loanPurpose = action.payload.purpose;
      }
    },
    payLoan: (state) => {
      state.loan = 0;
      state.loanPurpose = '';
      state.balance -= state.loan;
    },
  },
});
```

**Step 4: Export the Slice**

1. Export the reducer and actions from the slice.

```javascript
export default accountSlice.reducer;
export const { deposit, withdraw, requestLoan, payLoan } = accountSlice.actions;
```

**Conclusion**

Redux Toolkit makes it easier to write state slices by providing a `createSlice` function that automatically generates action creators and simplifies reducer logic. This can save you time and effort, especially when working on large applications.

**Additional Notes**

* You can still write your own reducer functions if you prefer.
* You can still use the `combineReducers` function from classic Redux if you need to combine multiple slices into a single store.
* Redux Toolkit also provides other features, such as middleware and dev tools integration, that can make your Redux development experience even more enjoyable.

# Back to Thunks

Sure, here are detailed notes with code from the paragraph given below:

**Restoring Thunks in Redux Toolkit**

**Step 1: Reuse Existing Action Creators**

1. Redux Toolkit automatically provides Thunks, so there is no need to install anything.
2. You can reuse your existing action creators by copying and pasting them into your Redux Toolkit slice.
3. Make sure that the action creators have the same name and type as the reducers in your slice.

```javascript
// Reuse the deposit action creator
export const deposit = (amount, currency) => ({
  type: 'account/deposit',
  payload: {
    amount: amount,
    currency: currency,
  },
});
```

**Step 2: Create a Reducer for Currency Conversion**

1. Create a new reducer for currency conversion.
2. The reducer should set the `loading` state to `true` before the conversion and `false` after the conversion.

```javascript
const convertCurrency = (state) => {
  state.loading = true;
  // Convert currency here
  state.loading = false;
};
```

**Step 3: Export Action Creators and Reducer**

1. Export the action creators and reducer from your slice.

```javascript
export const { deposit, withdraw, requestLoan, payLoan } = accountSlice.actions;
export default accountSlice.reducer;
export const convertCurrency = accountSlice.actions.convertCurrency;
```

**Conclusion**

Redux Toolkit makes it easy to use Thunks without any additional setup. You can reuse your existing action creators and create new reducers for specific tasks. This flexibility makes Redux Toolkit a powerful tool for managing asynchronous operations in your Redux applications.

**Additional Notes**

* You can use the `createAsyncThunk` function from Redux Toolkit if you prefer to have more control over your Thunk actions.
* Redux Toolkit automatically integrates with React DevTools, so you can debug your Thunk actions and see their state changes in the browser.
* Redux Toolkit provides a number of other features, such as middleware and dev tools integration, that can make your Redux development experience even more enjoyable.

# Creating the Customer Slice

Sure, here are detailed notes with code from the paragraph given below:

**Converting the Customer Slice to Redux Toolkit**

**Step 1: Create the Slice**

1. Call the `createSlice` function and pass it an object of options.
2. The `name` property should specify the name of the slice.
3. The `initialState` property should specify the initial state of the slice.
4. The `reducers` property should specify an object of reducers.

```javascript
const customerSlice = createSlice({
  name: 'customer',
  initialState: {
    customers: [],
  },
  reducers: {
    createCustomer: (state, action) => {
      state.customers.push({
        fullName: action.payload.fullName,
        nationalID: action.payload.nationalID,
        createdAt: new Date().toISOString(),
      });
    },
    updateName: (state, action) => {
      const customerIndex = state.customers.findIndex(customer => customer.nationalID === action.payload.nationalID);
      state.customers[customerIndex].fullName = action.payload.fullName;
    },
  },
});
```

**Step 2: Prepare Action Payloads**

1. Create a prepare function for each action creator that requires data preparation.
2. The prepare function should return an object containing the payload data.

```javascript
// Prepare payload for createCustomer action creator
const prepareCreateCustomerPayload = (fullName, nationalID) => ({
  fullName,
  nationalID,
  createdAt: new Date().toISOString(),
});
```

**Step 3: Export Action Creators and Reducer**

1. Export the action creators and reducer from the slice.

```javascript
export const { createCustomer, updateName } = customerSlice.actions;
export default customerSlice.reducer;
```

**Conclusion**

Redux Toolkit simplifies the process of creating slices by providing a `createSlice` function that automatically generates action creators and reduces boilerplate code. The use of prepare functions for data preparation further enhances the flexibility and organization of Redux actions. This streamlined approach makes Redux Toolkit a valuable tool for managing state in your React applications.

**Additional Notes**

* You can still write your own reducer functions if you prefer.
* You can still use the `combineReducers` function from classic Redux if you need to combine multiple slices into a single store.
* Redux Toolkit also provides other features, such as middleware and dev tools integration, that can make your Redux development experience even more enjoyable.

# Redux vs. Context API

Sure, here are detailed notes with code from the paragraph given below:

**Comparing Redux with React's Context API**

**Overview**

Redux and React's Context API are both solutions for managing global state in React applications. They each have their own strengths and weaknesses, making them suitable for different use cases.

**Advantages of Context API + useReducer**

* Built-in to React, no additional packages required
* Straightforward setup for single context and useReducer
* Simple for sharing values that don't change often, such as app color theme, language, or authenticated user

**Disadvantages of Context API + useReducer**

* Can lead to "provider hell" with multiple state slices
* No built-in mechanism for async operations
* Performance optimization requires more effort compared to Redux
* Limited DevTools compared to Redux

**Advantages of Redux**

* Initial setup can be more complex, but easier to manage additional state slices
* Built-in support for middleware to handle asynchronous operations
* Highly optimized for frequent state updates, minimizing wasted renders
* Excellent DevTools for debugging and inspecting state

**Disadvantages of Redux**

* Requires additional packages and increases bundle size
* More complex to implement and understand compared to Context API

**Usage Recommendations**

* **Context API + useReducer:**
    * Small applications
    * Sharing values that don't change often
    * Simple prop drilling problems
    * Managing state in local sub-trees of the application

* **Redux:**
    * Large applications with complex UI state
    * Frequent state updates (shopping carts, open tabs, data filters)
    * Complex state with nested objects

**Conclusion**

The choice between Redux and Context API depends on the specific needs of your project. Carefully consider the factors mentioned above to determine which solution is best suited for your application.
