Redux is a core library and react-redux is a implementation of redux for wiring so redux and react can communicate.

Redux ek core library hai aur react-redux uska implementation hai wiring karne karne ke liye taaki react aur redux aapas me baat kar sake.

Har ek application me ek hi store hota hai use bolte hai single source of truth.

## Redux, React-Redux, Redux-Toolkit

Certainly, let's discuss these concepts in the context of React:

**Redux in React:**
In React applications, managing state becomes crucial as the app grows. Redux is a library used with React to centralize and organize the application's state. It provides a global store where all the data (state) of the application is kept.

- **Store:** The store is like a big container that holds all the data for the entire application.

- **Actions:** Actions are like messages that tell the store what happened. For example, a user clicking a button can trigger an action.

- **Reducers:** Reducers are functions that decide how the state should change based on the received actions. They take the current state and an action, and then return a new state.

**React Redux:**
React Redux is a package that helps integrate Redux with React. It provides a way for React components to interact with the Redux store.

- It uses the `connect` function to establish a connection between React components and the Redux store.
  
- Connected components can access the state from the store and dispatch actions to update the state.

**Redux Toolkit in React:**
Redux Toolkit is particularly helpful in simplifying Redux-related code in React applications.

- **configureStore():** It provides a simple way to set up the Redux store, reducing boilerplate code.

- **createSlice():** It makes writing reducers more straightforward. A slice includes the reducer logic and the actions in a more concise manner.

- **createAsyncThunk():** For handling asynchronous operations like API calls, this utility makes it cleaner and easier to manage in React applications.

So, in React, Redux helps manage the state, React Redux connects React components with the Redux store, and Redux Toolkit makes the use of Redux in React more convenient by providing useful utilities.


## Steps for using redux in react by creating todo app.

## Step 1:
create a folder named `app` in src. Inside `app` create a file `store.js`.
Inside `store.js`:
```javascript
import { configureStore } from "@reduxjs/toolkit";
import todoReducer from '../features/todo/todoSlice'

export const store = configureStore({
  reducer: todoReducer
})
```

## Step 2:
Create a folder named `features`, inside a `features` folder create a folder named `todo`, inside a `todo` folder create a file `todoSlice.js`.
Inside `todoSlice.js`:
```javascript
import { createSlice, nanoid } from "@reduxjs/toolkit";

// nanoid: It generates unique id.

const initialState = {
    todos: [{
        id: 1,
        text: "Hello World"
    }]
}

export const todoSlice = createSlice({
    name: 'todo',
    initialState,
    reducers: {
        addTodo: (state, action) => {
            // state -> current state
            // action -> data which will be passed
            const todo = {
                id: nanoid(),
                text: action.payload
            }
            state.todos.push(todo)
        },
        removeTodo: (state, action) => {
            state.todos = state.todos.filter((todo) => todo.id !== action.payload)
        },
    }
})

export const {addTodo, removeTodo} = todoSlice.actions

export default todoSlice.reducer
```

## Step 3:
Inside a `src` folder create a folder named `components` inside a `components` folder create a files named  `AddTodo.jsx` and `Todos.jsx`
Inside `AddTodo.jsx`:
```jsx
import React, {useState} from 'react'
import { useDispatch } from 'react-redux'
import {addTodo} from '../features/todo/todoSlice'

const AddTodo = () => {

    const [input, setInput] = useState('')
    const dispatch = useDispatch()

    const addTodoHandler = (e) => {
        e.preventDefault()
        dispatch(addTodo(input))
        setInput('')
    }

  return (
    <form onSubmit={addTodoHandler} className='space-x-3 mt-10'>
        <input 
            type="text"
            className='bg-gray-800 rounded border border-gray-700 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-900 text-base outline-none text-gray-100 py-1 px-3 leading-8 trasition-colors duration-200 ease-in-out'
            placeholder='Enter a Todo...' 
            value={input}
            onChange={(e) => setInput(e.target.value)}
        />
        <button 
            type='submit'
            className='text-whtie bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded text-lg'
        >Add Todo</button>
    </form>
  )
}

export default AddTodo
```

Inside `Todo.jsx`:
```jsx
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import {removeTodo} from '../features/todo/todoSlice'

function Todos() {
    const todos = useSelector(state => state.todos)
    const dispatch = useDispatch()

  return (
    <>
    <div>Todos</div>
    <ul className="list-none">
        {todos.map((todo) => (
          <li
            className="mt-4 flex justify-between items-center bg-zinc-800 px-4 py-2 rounded"
            key={todo.id}
          >
            <div className='text-white'>{todo.text}</div>
            <button
             onClick={() => dispatch(removeTodo(todo.id))}
              className="text-white bg-red-500 border-0 py-1 px-4 focus:outline-none hover:bg-red-600 rounded text-md"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                strokeWidth={1.5}
                stroke="currentColor"
                className="w-6 h-6"
              >
                <path
                  strokeLinecap="round"
                  strokeLinejoin="round"
                  d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                />
              </svg>
            </button>
          </li>
        ))}
      </ul>
    </>
  )
}

export default Todos
```

## Step 4:
Inside `App.jsx`:
```jsx
import React from 'react'
import './App.css'
import AddTodo from './components/AddTodo'
import Todos from './components/Todos'

const App = () => {
  return (
    <>
      <h1 className='text-2xl sm:text-3xl'>Redux Toolkit</h1>
      <AddTodo />
      <Todos />
    </>
  )
}

export default App
```

## Step 5: 
Inside `main.jsx`:
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import {Provider} from 'react-redux'
import {store} from './app/store'

ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>,
)
```


## Redux Toolkit

-> store
-> reducers
-> useSelector
-> useDispatch

## store, reducers: its completely a part of redux

## useSelecotr, useDispatch: its completely a part of react

## useDispatch reducers ka use karte hue store ke andar values me changes karta hai

## store, reducers, useSelector, useDispatch

In the context of Redux Toolkit and React, the terms "store," "reducers," `useSelector`, and `useDispatch` are fundamental concepts. Let's break down each of them:

1. **Store:**

   - The store is a central and immutable object in Redux that holds the entire state of the application. It allows access to the state and provides methods to dispatch actions, which trigger state changes. In Redux Toolkit, the store is typically configured using the `configureStore` function.

     ```javascript
     import { configureStore } from "@reduxjs/toolkit";
     import rootReducer from "./reducers";

     const store = configureStore({
       reducer: rootReducer,
       // Additional configuration options can be added here
     });

     export default store;
     ```

2. **Reducers:**

   - Reducers are functions responsible for specifying how the application's state changes in response to dispatched actions. In Redux Toolkit, reducers are often created using the `createSlice` function. Reducers take the current state and an action as arguments, and they return a new state.

     ```javascript
     import { createSlice } from "@reduxjs/toolkit";

     const counterSlice = createSlice({
       name: "counter",
       initialState: 0,
       reducers: {
         increment: (state) => state + 1,
         decrement: (state) => state - 1,
       },
     });

     export const { increment, decrement } = counterSlice.actions;
     export default counterSlice.reducer;
     ```

3. **`useSelector` Hook:**

   - `useSelector` is a hook provided by the `react-redux` library (not specifically Redux Toolkit) that allows React components to access the current state in the Redux store. It takes a selector function as an argument, which is a function that extracts a specific piece of state from the store.

     ```javascript
     import { useSelector } from "react-redux";

     const CounterComponent = () => {
       const counter = useSelector((state) => state.counter);

       return (
         <div>
           <p>{counter}</p>
         </div>
       );
     };
     ```

4. **`useDispatch` Hook:**

   - `useDispatch` is another hook provided by `react-redux` that allows React components to dispatch actions to the Redux store. It returns a reference to the `dispatch` function.

     ```javascript
     import { useDispatch } from "react-redux";
     import { increment } from "./counterSlice";

     const CounterComponent = () => {
       const dispatch = useDispatch();

       const handleIncrement = () => {
         dispatch(increment());
       };

       return (
         <div>
           <button onClick={handleIncrement}>Increment</button>
         </div>
       );
     };
     ```

In summary, the store holds the application state, reducers define how the state changes, `useSelector` allows components to access state values, and `useDispatch` enables components to dispatch actions to modify the state. When using Redux Toolkit, the `createSlice` function simplifies the creation of reducers, and `configureStore` is used to set up the Redux store.


## Redux
Redux is a state management library for JavaScript applications, commonly used with React for managing the state of a React application in a predictable way. It was inspired by the Flux architecture and designed to help manage the state of an application in a more organized and maintainable manner, especially as the application grows in complexity.

The key principles of Redux include:

1. **Single Source of Truth:** The entire state of the application is stored in a single JavaScript object, often referred to as the "store." This makes it easier to understand and manage the application's state.

2. **State is Read-Only:** The state in a Redux application is immutable, meaning that it cannot be directly modified. Instead, to change the state, you dispatch actions, which are plain JavaScript objects describing what should change.

3. **Changes are Made with Pure Functions:** To describe how the state should change in response to an action, you define pure functions called "reducers." Reducers take the current state and an action as arguments and return a new state based on those inputs.

4. **Predictable State Changes:** Since the state changes in response to actions and reducers are pure functions, the state changes are predictable and can be traced.

Redux is often used with React, but it can be used with any JavaScript framework or library. React-Redux is a separate library that connects React with Redux, providing a set of bindings to simplify the integration of Redux with React components.

In summary, Redux is a state management library that helps developers manage and update the state of their applications in a predictable and maintainable way, particularly in the context of complex or large-scale applications.


## React-Redux
`react-redux` is the official React binding for Redux, a state management library in JavaScript. Redux is often used with React to manage the state of a React application in a predictable and scalable way. `react-redux` provides a set of tools and components that make it easier to integrate Redux with React applications.

The main components and concepts in `react-redux` include:

1. **`<Provider>` Component:**
   - The `<Provider>` component is a higher-order component that wraps your entire React application. It takes a `store` prop, which is the Redux store. This component makes the Redux store available to all components in the application without having to pass it explicitly as a prop through each level of the component tree.

   ```jsx
   import { Provider } from 'react-redux';
   import store from './store';

   ReactDOM.render(
     <Provider store={store}>
       <App />
     </Provider>,
     document.getElementById('root')
   );
   ```

2. **`connect` Function:**
   - The `connect` function is a higher-order function provided by `react-redux` that allows React components to connect to the Redux store and access the state and actions. It takes two main arguments: `mapStateToProps` and `mapDispatchToProps`, which define how to map the state and actions to the component's props.

   ```jsx
   import { connect } from 'react-redux';

   const mapStateToProps = (state) => ({
     counter: state.counter,
   });

   const mapDispatchToProps = (dispatch) => ({
     increment: () => dispatch({ type: 'INCREMENT' }),
   });

   const CounterComponent = ({ counter, increment }) => (
     <div>
       <p>{counter}</p>
       <button onClick={increment}>Increment</button>
     </div>
   );

   export default connect(mapStateToProps, mapDispatchToProps)(CounterComponent);
   ```

3. **`useDispatch` and `useSelector` Hooks:**
   - In addition to the `connect` function, `react-redux` also provides hooks for functional components. The `useDispatch` hook allows functional components to dispatch actions, and the `useSelector` hook allows components to select data from the Redux store.

   ```jsx
   import { useDispatch, useSelector } from 'react-redux';

   const CounterComponent = () => {
     const dispatch = useDispatch();
     const counter = useSelector((state) => state.counter);

     const increment = () => {
       dispatch({ type: 'INCREMENT' });
     };

     return (
       <div>
         <p>{counter}</p>
         <button onClick={increment}>Increment</button>
       </div>
     );
   };
   ```

By using `react-redux`, developers can efficiently integrate Redux with React components, manage the application state, and handle actions in a more organized and scalable manner. It provides a convenient way to connect the powerful state management capabilities of Redux with the component-based architecture of React.


## Redux Toolkit
Redux Toolkit is an official package from the creators of Redux that provides a set of utilities and conventions to simplify the process of working with Redux. It aims to streamline the development of Redux applications by reducing boilerplate code and providing a standardized way to define actions, reducers, and store setup. Redux Toolkit is not a replacement for Redux but rather a set of tools built on top of Redux to enhance the development experience.

Key features and components of Redux Toolkit include:

1. **`configureStore` Function:**
   - `configureStore` is a utility function that combines the steps of creating a Redux store, setting up middleware, and applying additional configuration options. It simplifies the store setup process and automatically includes commonly used middleware, such as Redux Thunk for handling asynchronous actions.

   ```javascript
   import { configureStore } from '@reduxjs/toolkit';
   import rootReducer from './reducers';

   const store = configureStore({
     reducer: rootReducer,
   });

   export default store;
   ```

2. **Simplified Reducer Syntax:**
   - Redux Toolkit introduces a `createSlice` function that simplifies the creation of reducer functions. It allows developers to define the initial state, actions, and reducers in a more concise manner.

   ```javascript
   import { createSlice } from '@reduxjs/toolkit';

   const counterSlice = createSlice({
     name: 'counter',
     initialState: 0,
     reducers: {
       increment: (state) => state + 1,
       decrement: (state) => state - 1,
     },
   });

   export const { increment, decrement } = counterSlice.actions;
   export default counterSlice.reducer;
   ```

3. **Immutability Helpers:**
   - Redux Toolkit includes a set of immutability helpers, such as `createSlice` and `createAsyncThunk`, which help in reducing the need for manual immutability logic when updating the state.

4. **Async Action Handling:**
   - Redux Toolkit provides `createAsyncThunk` for handling asynchronous actions in a more structured way. It simplifies the process of managing loading, success, and error states for asynchronous operations.

   ```javascript
   import { createAsyncThunk } from '@reduxjs/toolkit';

   const fetchUser = createAsyncThunk('user/fetchUser', async (userId) => {
     const response = await api.getUserById(userId);
     return response.data;
   });
   ```

5. **Redux DevTools Integration:**
   - Redux Toolkit is designed to work seamlessly with the Redux DevTools extension, providing a better debugging experience.

Redux Toolkit is recommended for new Redux projects as it encapsulates best practices and conventions, making it easier for developers to get started with Redux and maintain a consistent structure throughout their applications. It doesn't replace the core concepts of Redux but rather enhances them, making development more efficient and reducing common pain points.


## Reducers
In Redux Toolkit, a reducer is a function that describes how the state of an application changes in response to dispatched actions. Reducers in Redux Toolkit are typically created using the `createSlice` function, which is part of the toolkit's utilities.

Here's an overview of how a reducer is defined using `createSlice`:

1. **Import `createSlice`:**
   ```javascript
   import { createSlice } from '@reduxjs/toolkit';
   ```

2. **Use `createSlice` to Define a Reducer:**
   ```javascript
   const counterSlice = createSlice({
     name: 'counter',
     initialState: 0,
     reducers: {
       increment: (state) => state + 1,
       decrement: (state) => state - 1,
       // Additional reducer logic can be defined here
     },
   });
   ```

   In the example above:
   - `name`: Specifies the name of the slice, which will be used as a prefix for action types generated by the slice.
   - `initialState`: Specifies the initial state of the slice.
   - `reducers`: An object where each key represents an action type, and the corresponding value is a reducer function. Reducer functions take the current state as an argument and return a new state.

3. **Export the Reducer and Actions:**
   ```javascript
   export const { increment, decrement } = counterSlice.actions;
   export default counterSlice.reducer;
   ```

   The `counterSlice.actions` object contains the action creators generated by `createSlice`, and `counterSlice.reducer` is the reducer function.

4. **Use in Store Configuration:**
   ```javascript
   import { configureStore } from '@reduxjs/toolkit';
   import counterReducer from './counterSlice';

   const store = configureStore({
     reducer: {
       counter: counterReducer,
       // Additional reducers can be added here
     },
   });

   export default store;
   ```

   The reducer can then be included in the Redux store configuration using `configureStore`. Multiple reducers can be combined into the store by providing an object where each key is associated with a specific reducer.

Using `createSlice` from Redux Toolkit simplifies the process of creating reducers by handling the generation of action types and action creators automatically. It encourages a more concise and structured approach to defining reducer logic and helps reduce boilerplate code associated with traditional Redux reducers.

