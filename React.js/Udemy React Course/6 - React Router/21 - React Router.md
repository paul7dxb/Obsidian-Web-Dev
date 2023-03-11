- Used to create Single Page Applications (SPA)
- [[React-Router|Main react-router notes]]
- Example Projects:
	- [Udemy Course Basics](https://github.com/paul7dxb/react-udemy-course/tree/master/react-router-basics)
	- [Udemy Course Practice](https://github.com/paul7dxb/react-udemy-course/tree/master/react-router-practice)

# Structure

- Create Routes in pages folder in src

![[Image_React_router_structure.png]]

# Using routes

- Define route path and what component should be loaded for the path when route active
- Store returned browser router
	- Tell react to load and render router
	- RouterProvider component

- Array definition of routes
```JSX
import {createBrowserRouter, RouterProvider } from 'react-router-dom'
import HomePage from './pages/Home';
import ProductsPage from './pages/Products';

//Create router
const router = createBrowserRouter([
  {path: '/', element: <HomePage />},
  {path: '/products', element: <ProductsPage />}
])

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

- Older version
	- createRoutesFromElements
![[Image_React_router_Old_Routes.png]]

```JSX
import {createBrowserRouter, createRoutesFromElements, RouterProvider, Route } from 'react-router-dom'
import HomePage from './pages/Home';
import ProductsPage from './pages/Products';

//Old approach
const routeDefinitions = createRoutesFromElements(
  <Route>
    <Route path='/' element={<HomePage />} />
    <Route path='/products' element={<ProductsPage />} />
  </Route>
)
const router = createBrowserRouter(routeDefinitions);
```

# Navigating Between Pages

- Direct links with a tags create a request for the HTML page to the server
	- Results in new application load
	- Unneccessary work and don't want context lost
- Prevent default request and let react router know about request
	- Import Link from react-router-dom
		- Listens for clicks on element
		- Prevents default HTTP request
		- Looks at link definitions and changes URL

```JSX
import { Link } from "react-router-dom";

const HomePage = () => {
  return (
    <>
      <h1>Home</h1>
      Go to <Link to="/products">the list of products</Link>
    </>
  );
};

export default HomePage;
```

# Add Navigation Wrapper

- Add extra route to definitions with blank definition path
	- Load wrapper in element
	- Set children property and add child elements
- Use **outlet** Component in root element to tell react where the children should be rendered
- Can create path dependent root layouts

```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { path: "/", element: <HomePage /> },
      { path: "/products", element: <ProductsPage /> },
    ],
  },
]);
```

Root.js:
```JSX
import { Outlet } from "react-router-dom"
import MainNavigation from "../components/MainNavigation"
import classes from './Root.module.css'

function RootLayout(){

    return (
        <>
        <MainNavigation/>
        <main className={classes.content}>

        <Outlet/>
        </main>
        </>
    )
}

export default RootLayout
```

## Nested Layout Routes

app.js:
```JSX

```

## Displaying the active page

- Navlink
	- Instead of Link
	- Set className with a function
	- isActive is reached using array destructuring

```JSX
import { NavLink } from "react-router-dom";
import classes from './MainNavigation.module.css'

function MainNavigation() {
  return (
    <header className={classes.header}>
      <nav>
        <ul className={classes.list}>
          <li> <NavLink to="/" className={({isActive}) => (isActive ? classes.active : undefined)}>Home</NavLink>  </li>
          <li> <NavLink to="/products" className={({isActive}) => (isActive ? classes.active : undefined)}>Products</NavLink>  </li>
        </ul>
      </nav>
    </header>
  );
}

export default MainNavigation
```

# Programmatic Navigation

- Forms / Timers navigation from within code
- useNavigate Hook
- Gives a navigate function
	- To switch to a different route programmatically

- Example:
	- Don't navigate with buttons this is an example

```JSX
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();

function navigateHandler(){
	navigate('/products')
}


<button onClick={navigateHandler}>Navigate</button>
```

# Dynamic Routes

- path parameter defined using :variablePathName
	- Tells react route dom that this part is dynamic
- Use useParams Hook to get dynamic data
	- JS object containing every dynamic path property

path:
```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { path: "/products/:productID", element: <ProductDetailPage /> }
    ],
  },
]);
```

ProductDetail.js
```JSX
import { useParams } from "react-router-dom";

function ProductDetailPage() {
  const params = useParams();

  return (
    <>
      <h1>Product Details</h1>
      <p> {params.productID} </p>
    </>
  );
}

export default ProductDetailPage;
```

# Dynamic Links

- Using Dynamic routes will usually need generated links in a parent component

```JSX
import { Link } from "react-router-dom";

const PRODUCTS = [
  { id: "p1", title: "Product 1" },
  { id: "p2", title: "Product 2" },
  { id: "p3", title: "Product 3" },
];

function ProductsPage() {
  return (
    <>
      <h1>The products page</h1>
      <ul>
        {PRODUCTS.map((product) => (
          <li key={product.id}>
            <Link to={`/products/${product.id}`} >{product.title}</Link>
          </li>
        ))}
      </ul>
    </>
  );
}

export default ProductsPage;
```

