Sure, here are the notes from the paragraph with code if necessary:

**Creating the Redux Store**

1. Install the Redux package using `npm install Redux`.
2. Import the `createStore` function from Redux.
3. Create the store using the `createStore` function and the reducer function:

```javascript
const store = createStore(reducer);
```

4. Dispatch actions to the store to update the state:

```javascript
store.dispatch({ type: 'account.deposit', payload: 500 });
store.dispatch({ type: 'account.withdraw', payload: 200 });
store.dispatch({
  type: 'account.requestLoan',
  payload: { amount: 1000, purpose: 'buy a car' },
});
store.dispatch({ type: 'account.payLoanBack' });
```

5. Log the store state to the console to verify the changes:

```javascript
console.log(store.getState());
```

**Next Steps**

1. Create action creators to automate the process of creating actions.
2. Implement the action types for `account.requestLoan`.
