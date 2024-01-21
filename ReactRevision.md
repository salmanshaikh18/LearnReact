## Create Custom React

### index.html : 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="root"></div>
    <script src="./customReact.js"></script>
</body>
</html>
```

### renderReact.js : 
```Javascript
const reactElement = {
    type: 'a',
    props: {
        href: 'https://www.google.com',
        target: '_blank'
    },
    children: 'I am a Google.'
}

const mainContainer = document.querySelector('#root')

const customRender = (reactElement, mainContainer) => {
    const domElement = document.createElement(reactElement.type)
    domElement.innerHTML = reactElement.children
    // domElement.setAttribute('href', reactElement.props.href)
    // domElement.setAttribute('target', reactElement.props.target)
    for (prop in reactElement.props) {
        if (prop == reactElement.children) continue;
        domElement.setAttribute(prop, reactElement.props[prop])
    }
    mainContainer.appendChild(domElement)
}

customRender(reactElement, mainContainer)
```


## Babel in web dev

Babel is a popular JavaScript compiler used in web development. Its primary purpose is to transform ECMAScript 2015+ (ES6 and later) code into a backward-compatible version of JavaScript that can run in older browsers or environments that do not support the latest ECMAScript features.

Here are some key points about Babel:

1. **ECMAScript Compatibility:** Babel allows developers to write code using the latest ECMAScript syntax and features, even if the target environment supports only older versions of JavaScript. It helps bridge the gap between what developers write and what browsers can interpret.

2. **Transpilation:** Babel performs a process called transpilation, which is a combination of "transformation" and "compilation." It takes the modern JavaScript code and converts it into an equivalent version that works in older browsers or environments.

3. **Plugin System:** Babel is highly extensible and customizable through its plugin system. Developers can use plugins to add or customize specific transformations. This flexibility allows Babel to adapt to various project requirements.

4. **Integration with Build Tools:** Babel is often integrated into build tools such as webpack, Rollup, or npm scripts. This integration enables automatic code transformation during the build process, ensuring that the generated code is compatible with the target environment.

5. **Support for JSX:** Babel is commonly used with React applications to transpile JSX (JavaScript XML), a syntax extension that allows developers to write HTML-like code within JavaScript.

To use Babel in a project, you typically need to install it as a dependency, configure it with a `.babelrc` (Babel configuration) file, and integrate it into your build process. This process ensures that your modern JavaScript code is transformed into a version compatible with a broader range of browsers.

Example `.babelrc` configuration:

```json
{
  "presets": ["@babel/preset-env"]
}
```

In this example, the `@babel/preset-env` preset is used to automatically determine the plugins needed based on the target environment specified in the configuration.


## Babel in React

In a React project, Babel plays a crucial role in transforming the JSX (JavaScript XML) syntax and modern JavaScript features used in React components into a format that can be understood by browsers, especially those that do not support the latest ECMAScript features and JSX.

Here's what Babel does in a React project:

1. **JSX Transformation:**
   - React components often use JSX syntax, which allows developers to write XML-like code within JavaScript. JSX is not natively supported by browsers.
   - Babel transforms JSX code into plain JavaScript. It converts JSX elements into `React.createElement` function calls, which are then executed by the React runtime.

   Example JSX code:

   ```jsx
   const element = <h1>Hello, React!</h1>;
   ```

   Transformed JavaScript code:

   ```javascript
   const element = React.createElement('h1', null, 'Hello, React!');
   ```

2. **ES6+ Transformation:**
   - Babel also transpiles modern ECMAScript features (ES6 and later) into a version of JavaScript compatible with a wider range of browsers.
   - It allows developers to use features like arrow functions, destructuring assignment, let and const declarations, and other ES6+ syntax in their React code.

   Example ES6+ code:

   ```jsx
   const myFunction = (name) => {
     console.log(`Hello, ${name}!`);
   };
   ```

   Transformed JavaScript code:

   ```javascript
   var myFunction = function myFunction(name) {
     console.log('Hello, ' + name + '!');
   };
   ```

3. **React Preset:**
   - Babel provides a preset specifically designed for React projects, known as `@babel/preset-react`.
   - This preset includes the necessary plugins to handle JSX transformation and other React-specific optimizations.

   Example Babel configuration with React preset:

   ```json
   {
     "presets": ["@babel/preset-env", "@babel/preset-react"]
   }
   ```

4. **Integration with Build Tools:**
   - Babel is often integrated into build tools like webpack, Rollup, or other bundlers.
   - During the build process, Babel is applied to the React code, transforming it into a format that can be safely executed across various browsers.

In summary, Babel is an essential tool in a React project, ensuring that developers can write React components using the latest JavaScript features and JSX syntax, while still producing code that is compatible with a broad range of browsers. The configuration typically includes the `@babel/preset-react` preset along with `@babel/preset-env` for broader ECMAScript compatibility.



## React Fiber

React Fiber is an internal architecture of the React library designed to enhance the performance and responsiveness of React applications. It was introduced in React version 16.0 as a complete rewrite of the core algorithm responsible for updating and rendering components. The name "Fiber" refers to a set of techniques for improving the way React performs reconciliation, rendering, and updates.

Key concepts and features of React Fiber include:

1. **Incremental Rendering:**
   - One of the primary goals of React Fiber is to enable incremental rendering. Instead of completing the entire reconciliation and rendering process in one go, Fiber allows React to work on rendering a small unit of work, known as a "fiber," and then yield control to the main thread. This helps in creating smoother user experiences, especially in complex and dynamic applications.

2. **Prioritization:**
   - Fiber introduces the concept of priority to tasks in the reconciliation process. Different tasks (such as handling user interactions, animations, or network requests) are assigned priorities based on their importance. React can then prioritize high-priority tasks to ensure that critical updates are processed more quickly.

3. **Virtual Stack Frame:**
   - Fiber uses a virtual stack frame to keep track of the execution context during reconciliation. This allows React to pause and resume work, facilitating the interruption of tasks and enabling the implementation of features like suspense and error boundaries.

4. **Concurrent Mode:**
   - Concurrent Mode is a set of new features enabled by the React Fiber architecture. It allows React to work on multiple tasks simultaneously, even if they are part of the same update. Concurrent Mode is particularly useful for creating responsive user interfaces that can handle complex workloads without sacrificing performance.

5. **Error Boundaries and Improved Error Handling:**
   - React Fiber improves error handling by introducing error boundaries. Error boundaries are components that can catch JavaScript errors anywhere in their component tree and log those errors, display fallback UI, or take other actions. This helps prevent an entire component tree from failing due to an error in one part.

6. **Better Support for Asynchronous Rendering:**
   - Fiber lays the groundwork for better support of asynchronous rendering patterns. This is crucial for implementing features like suspense, which allows components to "suspend" rendering while waiting for data.

It's important to note that React Fiber is mostly an internal implementation detail of React, and developers typically interact with the React library without needing to be aware of its specifics. However, the improvements introduced by React Fiber contribute to the overall performance and user experience of React applications. As of my last knowledge update in January 2022, React Fiber continues to be a foundational part of the React library.


## useCallback()

In React.js, the `useCallback` hook is used to memoize a callback function. Memoization is a technique where the result of a function is cached and returned when the same inputs occur again, instead of recomputing the result. This can be useful in optimizing performance, particularly in scenarios where a function is passed down to child components.

Here's a typical use case for `useCallback`:

```jsx
import React, { useState, useCallback } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  // Without useCallback, a new function is created on every render
  // This can lead to unnecessary re-renders of child components
  const handleClick = () => {
    setCount(count + 1);
  };

  // With useCallback, the function is memoized and only changes
  // if the dependencies in the second argument change
  const memoizedHandleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      {/* Without useCallback */}
      <button onClick={handleClick}>Increment</button>
      {/* With useCallback */}
      <button onClick={memoizedHandleClick}>Increment (Memoized)</button>
    </div>
  );
}
```

In the example above, the `handleClick` function is created on each render, potentially causing unnecessary re-renders of child components that receive this function as a prop. By using `useCallback`, the function is only recreated if the dependencies (in this case, `[count]`) change. This can help in optimizing performance, especially in scenarios where the callback is passed to child components that use `React.memo` or have their own `shouldComponentUpdate` optimizations.


## useRef()

In React, the `useRef` hook is used to create a mutable object called a "ref" that can persist across renders of a functional component. The primary use cases for `useRef` include accessing and interacting with the DOM, managing focus, and persisting values across renders without causing re-renders.

Here are some common use cases for `useRef`:

1. **Accessing DOM Elements:**
   `useRef` can be used to obtain a reference to a DOM element. This is useful for interacting with the DOM directly, such as reading or modifying the DOM element properties.

   ```jsx
   import React, { useRef, useEffect } from 'react';

   function MyComponent() {
     const myInputRef = useRef();

     useEffect(() => {
       // Focus on the input element when the component mounts
       myInputRef.current.focus();
     }, []);

     return <input ref={myInputRef} />;
   }
   ```

2. **Storing Mutable Values without Triggering Re-renders:**
   Unlike state, updating the value of a `ref` does not cause the component to re-render. This makes `useRef` suitable for storing values that you don't want to trigger re-renders.

   ```jsx
   import React, { useRef, useEffect } from 'react';

   function MyComponent() {
     const counterRef = useRef(0);

     useEffect(() => {
       // This effect will not re-run if counterRef.current changes
       console.log("Current counter value:", counterRef.current);
     }, []);

     return (
       <button onClick={() => counterRef.current++}>
         Increment Counter
       </button>
     );
   }
   ```

3. **Preserving Values across Renders:**
   Since the value stored in a `ref` persists across renders, it can be useful for preserving values that shouldn't trigger a re-render when changed.

   ```jsx
   import React, { useRef, useEffect } from 'react';

   function MyComponent() {
     const previousValueRef = useRef();

     useEffect(() => {
       // Save the current value to the ref after each render
       previousValueRef.current = someValue;
     }, [someValue]);

     return <div>Previous Value: {previousValueRef.current}</div>;
   }
   ```

It's important to note that `useRef` does not cause re-renders when its value changes, making it different from the `useState` hook. Instead, it provides a way to persist values across renders and interact with the DOM in a functional component.