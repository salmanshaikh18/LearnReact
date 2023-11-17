# React Router DOM

## What is Routing ?

-> Routing in React is the process of determining which components to render based on the current URL or route.

-> React Router DOM  is an npm package that enables us to implement dynamic routing in a web app.

-> It allows us to display pages and allow users to navigate them.


## Difference between dynamic routing and static routing.

-> Dynamic routing allows you to handle different content based on the specific URL accessed, often involving parameters. It's flexible and can adapt to various situations during runtime.

-> Static routing involves predefined routes where the content associated with each route is fixed and known at compile-time. The routing structure remains constant during the application's execution.


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


## Configuring the Router

-> We have to import createBrowserRouter from 'react-router-dom'

-> createBrowserRouter allows us to define the routes as an array of object in which we can specify a path, the elements to be rendered when the path is browsed 


## Problems with <a> tag

-> It will reload the entire page when it is clicked.

-> It disrupts user experience and can result in a slower page load time.

-> This causes problems for single page applications(SPAs).

-> So to solve this issue, react-router-dom gives us a `Link`.


## Nested Routing

-> Nested routing means routes inside another route.

-> An <Outlet> should be used in parent route elements to render their child route elements.

-> This allows nested UI to show up when child routes are rendered.

-> If the parent route matched exactly, it will render a child index route or nothing if there is no index route.


## Link

A <Link> is an element that lets the user navigate to another page by clicking or tapping on it. In react-router-dom, a <Link> renders an accessible <a> element with a real href that points to the resource it's linking to. This means that things like right-clicking a <Link> work as you'd expect. You can use <Link reloadDocument> to skip client side routing and let the browser handle the transition normally (as if it were an <a href>).

In React with React Router DOM, the `<Link>` tag is specifically used to create clickable links for navigation within your application. Here are its main uses:

1. **Declarative Navigation:** `<Link>` allows you to define navigation in a declarative way. Instead of manually handling events or changing the URL through JavaScript, you declare links that users can click to navigate.

   ```jsx
   import { Link } from 'react-router-dom';

   // ...

   <Link to="/about">Go to About</Link>
   ```

2. **Preventing Full Page Reloads:** When a user clicks a `<Link>`, React Router DOM prevents the entire page from reloading. It updates the view efficiently and only replaces the content that needs to change, providing a smoother user experience.

3. **Dynamic Routing:** `<Link>` works seamlessly with React Router's dynamic routing. You can include route parameters in the `to` prop to create dynamic links that adapt to different data or conditions.

   ```jsx
   <Link to={`/user/${userId}`}>User Profile</Link>
   ```

4. **Navigation Without Page Refresh:** Since React Router DOM is designed for single-page applications, using `<Link>` ensures that navigation happens without a full page refresh. This is crucial for creating a fast and responsive user interface.

In summary, the `<Link>` tag in React Router DOM is a fundamental tool for building navigational elements in your application, providing a user-friendly and efficient way to move between different views or pages.


# NavLink

In React Router DOM, the `NavLink` component serves a similar purpose to the `Link` component, but with additional features tailored for navigation. Here are some key uses of `NavLink`:

1. **Active Styles:** `NavLink` allows you to apply specific styles to the link when it matches the current URL. This is helpful for highlighting the active link in your navigation.

   ```jsx
   import { NavLink } from 'react-router-dom';

   // ...

   <NavLink to="/home" activeClassName="activeLink">Home</NavLink>
   ```

   With the above example, when the URL is "/home," the "activeLink" class will be applied to the `NavLink` component.

2. **Active Classname:** Instead of inline styles, you can use the `activeClassName` prop to specify the class name that should be applied when the link is active.

   ```jsx
   <NavLink to="/about" activeStyle={{ fontWeight: 'bold', color: 'red' }}>About</NavLink>
   ```

   In this case, when the link is active, it will have bold text and a red color.

3. **Exact Matching:** `NavLink` has an `exact` prop that, when set to `true`, ensures that the link is active only when the URL matches exactly.

   ```jsx
   <NavLink to="/" exact>Home</NavLink>
   ```

   This prevents partial matches and helps in scenarios where you want to highlight the "Home" link only when the URL is exactly "/".

4. **Custom Active Condition:** You can use the `isActive` prop to define a custom condition for determining whether the link is active.

   ```jsx
   <NavLink
     to="/products"
     isActive={(match, location) => {
       // Custom condition, e.g., only activate link on certain pages
       return match !== null && location.pathname.startsWith('/products');
     }}
   >
     Products
   </NavLink>
   ```

These features make `NavLink` a powerful tool for creating dynamic and interactive navigation in React applications, providing enhanced styling and control over active links.


## Outlet

In React Router DOM, the `<Outlet>` component is used in conjunction with the `<Route>` component to handle nested route rendering. Here are the main uses of `<Outlet>`:

1. **Nested Routing:** `<Outlet>` is primarily used when you have nested routes within your application. It acts as a placeholder where child routes can be rendered.

   ```jsx
   // ParentRoute component
   import { Outlet } from 'react-router-dom';

   const ParentRoute = () => (
     <div>
       <h2>Parent Route</h2>
       <Outlet /> {/* Placeholder for child routes */}
     </div>
   );
   ```

2. **Rendering Child Routes:** Child routes are defined within the parent route component. The `<Outlet>` component is the place where these child routes will be rendered.

   ```jsx
   // App component
   import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
   import ParentRoute from './ParentRoute';
   import ChildRoute1 from './ChildRoute1';
   import ChildRoute2 from './ChildRoute2';

   const App = () => (
     <Router>
       <Routes>
         <Route path="/" element={<ParentRoute />}>
           <Route index element={<ChildRoute1 />} />
           <Route path="child2" element={<ChildRoute2 />} />
         </Route>
       </Routes>
     </Router>
   );
   ```

   Here, `<Outlet>` in `ParentRoute` is where the child routes (`ChildRoute1` and `ChildRoute2`) will be inserted based on the matching route.

3. **Dynamic Route Nesting:** `<Outlet>` allows you to dynamically nest routes based on the URL. This is useful when you have varying levels of nested routes.

   ```jsx
   // DynamicRoute component
   import { Outlet, useParams } from 'react-router-dom';

   const DynamicRoute = () => {
     const { id } = useParams();
     
     return (
       <div>
         <h3>Dynamic Route {id}</h3>
         <Outlet /> {/* Placeholder for further nested routes */}
       </div>
     );
   };
   ```

   Here, `<Outlet>` can be used to render additional nested routes specific to the dynamic route.

In summary, `<Outlet>` is a crucial component in React Router DOM for handling nested routes. It provides a way to define where child routes should be rendered within a parent route, allowing for a structured and dynamic route configuration in your application.


## RouterProvider

All data router objects are passed to this component to render your app and enable the rest of the data APIs.

```javascript
import {
  createBrowserRouter,
  RouterProvider,
} from "react-router-dom";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    children: [
      {
        path: "dashboard",
        element: <Dashboard />,
      },
      {
        path: "about",
        element: <About />,
      },
    ],
  },
]);

ReactDOM.createRoot(document.getElementById("root")).render(
  <RouterProvider
    router={router}
  />
);
```