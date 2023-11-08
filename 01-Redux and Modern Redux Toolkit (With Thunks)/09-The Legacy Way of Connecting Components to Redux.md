**Connecting React Components to Redux Store with Connect API**

**Legacy Approach**

1. **Use Connect Function to Wrap Component:**
   ```javascript
   export default connect(mapStateToProps)(BalanceDisplay);
   ```

2. **Define mapStateToProps Function:**
   ```javascript
   const mapStateToProps = (state) => ({
     balance: state.account.balance,
   });
   ```

3. **Access State from Wrapped Component:**
   ```javascript
   const balance = props.balance;
   ```

**Modern Approach**

1. **Use useSelector Hook to Read State:**
   ```javascript
   const balance = useSelector((state) => state.account.balance);
   ```
