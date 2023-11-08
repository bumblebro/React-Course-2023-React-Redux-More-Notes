**Creating Customer State and Actions**

1. Define the initial state for the customer:

```javascript
const initialStateCustomer = {
  fullName: '',
  nationalID: '',
  createdAt: '',
};
```

2. Create action creators for customer-related actions:

```javascript
function createCustomer(fullName, nationalID) {
  return {
    type: 'customer/createCustomer',
    payload: {
      fullName,
      nationalID,
      createdAt: new Date().toISOString(),
    },
  };
}

function updateCustomerName(fullName) {
  return {
    type: 'customer/updateName',
    payload: {
      fullName,
    },
  };
}
```

3. Create a customer reducer:

```javascript
function customerReducer(state = initialStateCustomer, action) {
  switch (action.type) {
    case 'customer/createCustomer':
      return {
        ...state,
        fullName: action.payload.fullName,
        nationalID: action.payload.nationalID,
        createdAt: action.payload.createdAt,
      };
    case 'customer/updateName':
      return {
        ...state,
        fullName: action.payload.fullName,
      };
    default:
      return state;
  }
}
```

4. Create a root reducer that combines the account and customer reducers:

```javascript
const rootReducer = combineReducers({
  account: accountReducer,
  customer: customerReducer,
});
```

5. Use the root reducer to create the store:

```javascript
const store = createStore(rootReducer);
```

**Example Usage**

1. Dispatch an action to create a customer:

```javascript
store.dispatch(createCustomer('John Doe', '1234567890'));
```

2. Dispatch an action to update the customer's name:

```javascript
store.dispatch(updateCustomerName('Jane Doe'));
```

3. Get the current state of the store:

```javascript
console.log(store.getState());
```
