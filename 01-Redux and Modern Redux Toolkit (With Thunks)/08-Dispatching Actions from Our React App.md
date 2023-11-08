**Dispatching Actions to Redux Store from React Components**

1. **Use useDispatch Hook to Access Dispatch Function:**
   ```javascript
   const dispatch = useDispatch();
   ```

2. **Import Action Creators:**
   ```javascript
   import { createCustomer } from './customerSlice';
   ```

3. **Dispatch Actions:**
   ```javascript
   dispatch(createCustomer({ name: 'John Doe', nationalID: '123456789' }));
   ```

4. **Conditional Rendering:**
   ```javascript
   if (fullName === '') {
     return <CreateCustomer />;
   }
   return (
     <>
       <CustomerBalance balance={balance} />
       <CustomerOperations account={account} />
     </>
   );
   ```

5. **Dispatching Account Operations Actions:**
   ```javascript
   dispatch(deposit({ amount: 100 }));
   dispatch(withdraw({ amount: 50 }));
   dispatch(requestLoan({ amount: 1000, purpose: 'Buy a car' }));
   ```

6. **Reading Account Data from State:**
   ```javascript
   const account = useSelector((state) => state.account);
   ```

7. **Destructuring Account Data:**
   ```javascript
   const { balance, loan } = account;
   ```
