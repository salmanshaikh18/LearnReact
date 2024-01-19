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