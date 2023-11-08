**Organizing Code into Features**

- Create a `features` folder to house all feature-related code
- Within the `features` folder, create separate folders for each feature, such as `account` and `customer`
- Move components related to each feature into their respective folders
- Update imports to reflect the new file structure

**Organizing Redux Code**

- Create separate files for each feature's Redux logic (reducers, action creators, initial state)
- For each feature, export the reducers and action creators from their respective files
- In the main Redux file, import the reducers from each feature file and combine them into a single root reducer
- Export the root reducer from the main Redux file

**Updating Components to Use Redux**

- Import the action creators from the feature-specific files into the components that need to use them
- Dispatch actions using the action creators within the components

**Example Code**

```javascript
// features/account/accountSlice.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  balance: 0,
};

const accountSlice = createSlice({
  name: 'account',
  initialState,
  reducers: {
    deposit: (state, action) => {
      state.balance += action.payload;
    },
  },
});

export const { deposit } = accountSlice.actions;
export default accountSlice.reducer;
```

```javascript
// features/customer/customerSlice.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  name: '',
};

const customerSlice = createSlice({
  name: 'customer',
  initialState,
  reducers: {
    setName: (state, action) => {
      state.name = action.payload;
    },
  },
});

export const { setName } = customerSlice.actions;
export default customerSlice.reducer;
```

```javascript
// store.js
import { combineReducers } from 'redux';
import accountReducer from '../features/account/accountSlice';
import customerReducer from '../features/customer/customerSlice';

const rootReducer = combineReducers({
  account: accountReducer,
  customer: customerReducer,
});

export default rootReducer;
```

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { createStore } from 'redux';
import rootReducer from './store';
import App from './App';

const store = createStore(rootReducer);

store.dispatch({ type: 'account/deposit', payload: 250 });
console.log(store.getState());

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
