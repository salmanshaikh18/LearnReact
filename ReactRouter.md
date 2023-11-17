# React Router DOM

## What is Routing ?

-> Routing in React is the process of determining which components to render based on the current URL or route.

-> React Router DOM  is an npm package that enables us to implement dynamic routing in a web app.

-> It allows us to display pages and allow users to navigate them.


## Difference between dynamic routing and static routing.

Dynamic routing allows you to handle different content based on the specific URL accessed, often involving parameters. It's flexible and can adapt to various situations during runtime.
Example: 


Static routing involves predefined routes where the content associated with each route is fixed and known at compile-time. The routing structure remains constant during the application's execution.


## Dynamic Routing

In React, dynamic routing refers to the process of defining and handling routes in a way that allows for dynamic content rendering based on the requested URL. React Router is a popular library for implementing routing in React applications, and it provides a way to handle dynamic routing.

Dynamic routing is essential when you want to create components that can be reused for different data or situations, and the content of the components depends on the route parameters. Here's a brief overview of dynamic routing in React using React Router:

1. **Route Parameters:**
   React Router allows you to define dynamic segments in your routes using colons (`:`) followed by a parameter name. For example:

   ```jsx
   <Route path="/users/:id" component={UserProfile} />
   ```

   Here, `:id` is a route parameter, and it can take different values depending on the actual URL.

2. **Accessing Route Parameters:**
   You can access the route parameters in your components using the `useParams` hook provided by React Router. For functional components, you can do something like this:

   ```jsx
   import { useParams } from 'react-router-dom';

   function UserProfile() {
     const { id } = useParams();

     // Now 'id' contains the value of the 'id' parameter from the URL
     // Use it to fetch user data or perform other dynamic actions
     // ...
   }
   ```

3. **Dynamic Rendering:**
   With the route parameters, you can dynamically render components or fetch data based on the current URL. For example, you might use the `id` parameter to fetch user data and display it in the `UserProfile` component.

   ```jsx
   function UserProfile() {
     const { id } = useParams();

     // Fetch user data based on the 'id' parameter
     // ...

     return (
       <div>
         <h2>User Profile</h2>
         <p>User ID: {id}</p>
         {/* Render user data */}
       </div>
     );
   }
   ```

By using dynamic routing and route parameters, you can create more flexible and reusable components in your React applications. React Router simplifies the process of handling these dynamic routes and provides hooks like `useParams` to make it easier to work with route parameters in your components.


## Static Routing

Static routing in React refers to the process of defining fixed routes for your application. In static routing, the route configurations are determined at compile-time, and the application knows in advance which components to render for each specific route. This is in contrast to dynamic routing, where the routing information may be determined at runtime based on factors like user input or data fetched from a server.

In a React application, static routing is commonly implemented using a library like React Router. Here's a basic example of static routing using React Router:

1. **Install React Router:**
   You need to install React Router in your project. You can do this using npm or yarn:

   ```bash
   npm install react-router-dom
   ```

   or

   ```bash
   yarn add react-router-dom
   ```

2. **Define Routes:**
   In your application, you would define your routes using the `Route` component provided by React Router. Each `Route` component corresponds to a specific URL path and specifies the React component to render when that path is matched.

   ```jsx
   import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
   import Home from './components/Home';
   import About from './components/About';
   import Contact from './components/Contact';

   function App() {
     return (
       <Router>
         <Switch>
           <Route path="/" exact component={Home} />
           <Route path="/about" component={About} />
           <Route path="/contact" component={Contact} />
         </Switch>
       </Router>
     );
   }
   ```

   In this example:
   - The route "/" is associated with the `Home` component.
   - The route "/about" is associated with the `About` component.
   - The route "/contact" is associated with the `Contact` component.

3. **Navigation:**
   To navigate between different routes, you can use the `Link` component provided by React Router. For example:

   ```jsx
   import { Link } from 'react-router-dom';

   function Navigation() {
     return (
       <nav>
         <ul>
           <li>
             <Link to="/">Home</Link>
           </li>
           <li>
             <Link to="/about">About</Link>
           </li>
           <li>
             <Link to="/contact">Contact</Link>
           </li>
         </ul>
       </nav>
     );
   }
   ```

   Clicking on these links will navigate to the corresponding routes without a full page reload.

Static routing is suitable for applications where the navigation structure is known in advance and doesn't change frequently during runtime. It is a straightforward and efficient way to handle routing in many scenarios.
