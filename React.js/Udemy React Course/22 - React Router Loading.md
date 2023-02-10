
React Route V6 or greater
- It is not optimal to make data requests when running the first loading of the component
- Example: getting posts for a page when that page is loading
		- Old way;
			- Render loading screen then fetch data then rerender screen
			- May be done using a useEffect method that is only called once on the initial loading
		- New way with react router:
			- Loader function is called when the page is navigated to
			- Instead get the data when the page is being navigated to

- Note:
	- Loader funciton is not a REACT component so cannot use state

# Implementation

- Loader property for path definition:
	- Takes a function to executre before page is loaded
	- Load and fetch data here
	- Returned value is made available to component and other places where it is needed

- useLoaderData() hook in component:
	- Gets closest loader data
	- React Router will also check for promises from async functions

**This example is a demonstartion of the process only. See [[#Placing Loader Code]] section below for cleaner code**

App.js:
```JSX
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { index: true, element: <HomePage /> },
      {
        path: "events",
        element: <EventsRootLayout />,
        children: [
          {
            index: true,
            element: <EventsPage />,
            loader: async () => {
              const response = await fetch("http://localhost:8080/events");

              if (!response.ok) {
                console.log("error")
                // ...
              } else {
                const resData = await response.json();
                return resData.events;
              }
            },
          },
          { path: ":eventID", element: <EventDetailPage /> },
```

EventsPage.js
```JSX
import { useLoaderData } from "react-router-dom";

import EventsList from "../components/EventsList";

function EventsPage() {
  const events = useLoaderData();

  return (
    <>
      <EventsList events={events} />
    </>
  );
}

export default EventsPage;
```

- Due to getting closest data it is possible to put the useLoaderData() in the EventsList component instead of passing it through as a prop

# Placing Loader Code

- Put loader code in component file
	- Export the loader function
- Import the function into the route defining file

Component:
```JSX
import { useLoaderData } from "react-router-dom";

import EventsList from "../components/EventsList";

function EventsPage() {
  const events = useLoaderData();

  return (
    <>
      <EventsList events={events} />
    </>
  );
}

export default EventsPage;

export async function loader () {
  const response = await fetch("http://localhost:8080/events");

  if (!response.ok) {
    console.log("error")
    // ...
  } else {
    const resData = await response.json();
    return resData.events;
  }
}

```

App.js

```JSX
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import RootLayout from "./pages/Root";
import HomePage from "./pages/HomePage";
import EventsPage, {loader as eventsLoader} from "./pages/EventsPage";
import EventDetailPage from "./pages/EventDetailPage";
import NewEventPage from "./pages/NewEventPage";
import EditEventPage from "./pages/EditEventPage";
import EventsRootLayout from "./pages/EventsRoot";

//Create router
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    children: [
      { index: true, element: <HomePage /> },
      {
        path: "events",
        element: <EventsRootLayout />,
        children: [
          {
            index: true,
            element: <EventsPage />,
            loader: eventsLoader,
          },
          { path: ":eventID", element: <EventDetailPage /> },
          { path: "new", element: <NewEventPage /> },
          { path: ":eventID/edit", element: <EditEventPage /> },
        ],
      },
      ,
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

# Returning response objects

- Response is a browser function
- This is client side code
- useLoaderData can be used to access the data in the response

```JSX
  const data = useLoaderData();
  const events = data.events;
```

# Dealing with data loading

- By default react router will wait for the data to be fetched before displaying the component
- Should display to the user that the loading is taking place

## Option 1

- Use hook
	- useNavigation hook has a state property
		- idle: dont have active route transition
		- loading: have an active transition and we are loading data
		- submitting: submitting data
	- Loading state will be visible on currently displayed state

Use in the root layout:
```JSX
import MainNavigation from '../components/MainNavigation'
import { Outlet, useNavigation } from 'react-router-dom';
import classes from './Root.module.css'

function RootLayout(){

    const navigation = useNavigation();
return(
    <>
    <MainNavigation/>
    <main className={classes.content}>
        {navigation.state === 'loading' && <p>Loading...</p> }
            <Outlet />
    </main>

    </>
)
}

export default RootLayout;
```

