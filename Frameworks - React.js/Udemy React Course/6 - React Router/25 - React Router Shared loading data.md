- Allows loaders to be reused across multiple components

- Create a new path that does not have an element
- Put the loader function in this route
- Create the children array with the routes that need access to the data

- Error reaching up to data loader
	- Searches for closest availbale data but for relative urls it may not reach parent

- Add id to route with loader
- Use Different Hook in component that loads the data
		- Replace useLoaderData with useRouteLoaderData()

Routes:
```JSX
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
            id: 'event-detail',
            loader: eventDetailsLoader,
            children: [
              {
                index: true,
                element: <EventDetailPage />,
              },
              { path: "edit", element: <EditEventPage /> },
            ],
          },
```

Components:
```JSX
import { json,  useParams, useRouteLoaderData } from "react-router-dom";
import EventItem from "../components/EventItem";

function EventDetailPage() {
  const params = useParams();
  const data = useRouteLoaderData('event-detail');

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