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
