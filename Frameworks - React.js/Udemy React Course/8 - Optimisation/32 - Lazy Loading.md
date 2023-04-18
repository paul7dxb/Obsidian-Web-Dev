- A part of the optimization process
- When building an application imports are merged into one file
	- This means all code files will have to be loaded before anything is displayed
- Useful for LARGER applications that have large amounts of network traffic

# Solution Lazy Loading

- Load in certin components when they are needed leading to an improvement in performance
	- Certain code should only be loaded when it is needed

# How to Use

- remove the usual import
- Add the import lazily by passing a function to the loader that calls the import dynamically
	- imports return a promise
- For components
	- use the lazy function from react
	- Use suspense around lazily loaded components until they load

Instead of:
```JSX
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

import BlogPage, { loader as postsLoader } from './pages/Blog';
import HomePage from './pages/Home';
import PostPage, { loader as postLoader } from './pages/Post';
import RootLayout from './pages/Root';

const router = createBrowserRouter([
  {
    path: '/',
    element: <RootLayout />,
    children: [
      {
        index: true,
        element: <HomePage />,
      },
      {
        path: 'posts',
        children: [
          { index: true, element: <BlogPage />, loader: postsLoader },
          { path: ':id', element: <PostPage />, loader: postLoader },
        ],
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

```JSX
import { lazy, Suspense } from "react";
import { createBrowserRouter, RouterProvider } from "react-router-dom";

// import BlogPage, { loader as postsLoader } from './pages/Blog';
import HomePage from "./pages/Home";
// import PostPage, { loader as postLoader } from "./pages/Post";
import RootLayout from "./pages/Root";

const BlogPage = lazy(() => import("./pages/Blog"));
const PostPage = lazy(() => import("./pages/Post"));

const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      {
        index: true,
        element: <HomePage />,
      },
      {
        path: "posts",
        children: [
          {
            index: true,
            element: (
              <Suspense fallback={ <p>Loading...</p> }>
                <BlogPage />
              </Suspense>
            ),
            loader: () =>
              import("./pages/Blog").then((module) => module.loader()),
          },
          {
            path: ":id",
            element: (
              <Suspense fallback={ <p>Loading...</p> }>
                <PostPage />
              </Suspense>
            ),
            loader: (meta) =>
              import("./pages/Post").then((module) => module.loader(meta)),
          },
        ],
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;

```

- Only once trying to visit blog page the loader function will be executed
- Component BlogPage will be loaded lazily
- meta used to pass in whole object that includes the required params for the loader

# Result

- Form viewing the network tab you can see that the functions are loaded lazily

![[Image_React_Lazy_Loading.png]]