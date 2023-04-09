# Wrap all routes

```JSX
import { Outlet } from "react-router-dom";
import classes from "./RootLayout.module.css";


const RootLayout = (props) => {
  return (
    <>
      <Navigation />
      <main className={classes.main}> <Outlet/> </main>
    </>
  );
};

export default RootLayout;
```

```JSX
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./pages/Home";
import ProductDetailPage from "./pages/ProductDetail";
import ProductsPage from "./pages/Products";
import RootLayout from "./pages/Root";

//Create router
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { index: true, element: <HomePage /> },
      { path: "products", element: <ProductsPage /> },
      { path: "products/:productID", element: <ProductDetailPage /> }
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```