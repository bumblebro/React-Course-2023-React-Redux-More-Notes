Sure, here are the notes from the paragraph with code if necessary:

**Learning Redux in Isolation**

1. Create a new React application using `create-react-app` and name it `redux-intro`.
2. Delete the unnecessary files from the starter files folder.
3. Create a new file called `store.js` to store the Redux code.
4. Define the initial state of the bank account:
    ```javascript
    const initialState = {
      balance: 0,
      loan: 0,
      loanPurpose: '',
    };
    ```
5. Define the reducer function:
    ```javascript
    const reducer = (state = initialState, action) => {
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
          // TODO: Implement this action
          return state;
        case 'account.payLoanBack':
          return {
            ...state,
            loan: 0,
            loanPurpose: '',
            balance: state.balance - state.loan,
          };
        default:
          return state;
      }
    };
    ```
6. The reducer function should be pure, meaning it should not modify the existing state or perform side effects.
7. The reducer function should return a new state object based on the current state and the action.
8. The reducer function should handle actions with different types, each representing a different event that can happen in the application.
9. The reducer function should return the original state if it does not recognize the action type.

**Next Steps**

1. Create the Redux store using the reducer function.
2. Integrate the Redux store with the React application.
