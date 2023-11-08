**Creating Action Creators**

1. Action creators are functions that return actions.
2. They are a convention, not a requirement, of Redux.
3. They make the code more reusable and less error-prone.
4. They are typically created for each possible action.
5. To use an action creator, simply call it with the necessary arguments and pass the result to `store.dispatch`.

**Example Action Creators**
```javascript
function deposit(amount) {
  return { type: 'account.deposit', payload: amount };
}

function withdraw(amount) {
  return { type: 'account.withdraw', payload: amount };
}

function requestLoan(amount, purpose) {
  return { type: 'account.requestLoan', payload: { amount, purpose } };
}

function payLoan() {
  return { type: 'account.payLoanBack' };
}
```

**Using Action Creators**
```javascript
store.dispatch(deposit(500));
store.dispatch(withdraw(200));
store.dispatch(requestLoan(1000, 'Buy a cheap car'));
store.dispatch(payLoan());
```

**Old-Style Action Creator Usage**
```javascript
const ACCOUNT_DEPOSIT = 'account.deposit';

function deposit(amount) {
  return { type: ACCOUNT_DEPOSIT, payload: amount };
}
```

**Next Steps**

1. Add more state to the store.
2. Implement the action types for `account.requestLoan`.
