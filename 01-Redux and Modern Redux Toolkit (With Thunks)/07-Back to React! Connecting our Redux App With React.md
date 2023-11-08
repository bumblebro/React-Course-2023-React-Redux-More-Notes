**Connecting Redux Store with React Application**

1. **Install React Redux Package:**
   ```bash
   npm install react-redux
   ```

2. **Provide Store to the Application:**
   ```javascript
   import { Provider } from 'react-redux';

   const App = () => (
     <Provider store={store}>
       <AppContent />
     </Provider>
   );
   ```

3. **Read Data from Redux Store:**
   ```javascript
   import React from 'react';
   import { useSelector } from 'react-redux';

   const Customer = () => {
     const customer = useSelector((store) => store.customer);
     const fullName = `${customer.firstName} ${customer.lastName}`;

     return (
       <div>
         Welcome {fullName}!
       </div>
     );
   };
   ```

4. **Dispatch Actions to the Store:**
   (Next video)
