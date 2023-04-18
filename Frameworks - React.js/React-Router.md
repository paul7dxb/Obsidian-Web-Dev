- Allows creation of a single page application
- [Official docs](https://reactrouter.com/en/main)

Multi Page application
![[Image_Multi_Page_App.png]]

Single Page Application (SPA)

- One intial HTML request & response
- Load different content based on the path

![[Image_Single_Page_App.png]]

# Installation

```bash
npm install react-router-dom
```

# Path specifity

- React is smart enough to realise that specific paths should be rendred over varibale routes

```JSX
{ path: "events/:eventID", element: <EventDetailPage /> },
//Is less specific than
{ path: "events/new", element: <NewEventPage /> },
//So events/new will be reached
```

# Absolute vs Relative paths

- When referencing a path from / it is an **absolute path** from the domain name
	- Get an error if child routes have a different absolute path
- For child routes you can use relative paths that adopt the wrapper route path

- For child route the parent route is the parent path
	- For Links they can be made relative to root (parent path) or relative to path (relative to current path)
- Links to .. go to parent path

Absolute:
```JSX
const router = createBrowserRouter([
  {
    path: "/root",
    element: <RootLayout />,
    children: [
      { path: "/root", element: <HomePage /> },
      { path: "/root/products", element: <ProductsPage /> },
      { path: "/root/products/:productID", element: <ProductDetailPage /> }
    ],
  },
]);
```

Relative:
```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { path: "", element: <HomePage /> },
      { path: "products", element: <ProductsPage /> },
      { path: "products/:productID", element: <ProductDetailPage /> }
    ],
  },
]);
```

# Index Routes

- Where the path is the same as the parent route
	- The following are equivalent

```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { path: "", element: <HomePage /> },
      ...
```

```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { index: true, element: <HomePage /> },
      ...
```