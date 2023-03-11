- How to get the variable name intot the loader function?
	- Hooks can't be accessed
	- loader function contains
		- request
			- Query parmaters
		- params with all request parameters

-Steps:
	- Add loader function
	- Register in route definition
	- Pass response data to component

Routes:
```JSX
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import EventDetailPage, {
  loader as eventDetailsLoader,
} from "./pages/EventDetailPage";

//Create router
const router = createBrowserRouter([
  {
    path: "/",
    element: <RootLayout />,
    errorElement: <ErrorPage />,
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
          {
            path: ":eventID",
            loader: eventDetailsLoader,
            element: <EventDetailPage />,
          },
          ...
```

```JSX
import { json, useLoaderData, useParams } from "react-router-dom";
import EventItem from "../components/EventItem";

function EventDetailPage() {
  const params = useParams();
  const data = useLoaderData();

  return <EventItem event={data.event} />;
}

export default EventDetailPage;

export async function loader({ request, params }) {
  const id = params.eventID;
  const response = await fetch("http://localhost:8080/events/" + id);

  if (!response.ok) {
    throw json({ message: "Could not fetch details" }, { status: 500 });
  } else {
    return response;
  }
}
```