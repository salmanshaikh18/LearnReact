Redux is a core library and react-redux is a implementation of redux for wiring so redux and react can communicate.

Redux ek core library hai aur react-redux uska implementation hai wiring karne karne ke liye taaki react aur redux aapas me baat kar sake.

Har ek application me ek hi store hota hai use bolte hai single source of truth.

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
