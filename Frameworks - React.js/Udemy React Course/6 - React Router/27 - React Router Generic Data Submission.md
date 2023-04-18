- May be required to submit to differnt urls with different methods but for the same data
	- Form Component
		- Set the method the form will submit, may be passed in via props
	- Loader
		- Get the method from the request parameter
			- post
			- patch
		- Set the url based on the form method
	- Routes
		- Add action to routes that will require it

New Form and action:
```JSX
import { useNavigate, useNavigation, useActionData, json, redirect } from "react-router-dom";
import { Form } from "react-router-dom";

import classes from "./EventForm.module.css";

function EventForm({ method, event }) {
  const data = useActionData();
  const navigate = useNavigate();

  const navigation = useNavigation();
  const isSubmitting = navigation.state === "submitting";

  function cancelHandler() {
    navigate("..");
  }

  return (
    <Form method={method} className={classes.form}>
      {data && data.errors && (
        <ul>
          {Object.values(data.errors).map((err) => (
            <li key={err}> {err} </li>
          ))}
        </ul>
      )}
      <p>
        <label htmlFor="title">Title</label>
        <input
          id="title"
          type="text"
          name="title"
          defaultValue={event ? event.title : ""}
          required
        />
      </p>
      <p>
        <label htmlFor="image">Image</label>
        <input
          id="image"
          type="url"
          name="image"
          defaultValue={event ? event.image : ""}
          required
        />
      </p>
      <p>
        <label htmlFor="date">Date</label>
        <input
          id="date"
          type="date"
          name="date"
          defaultValue={event ? event.date : ""}
          required
        />
      </p>
      <p>
        <label htmlFor="description">Description</label>
        <textarea
          id="description"
          name="description"
          defaultValue={event ? event.description : ""}
          rows="5"
          required
        />
      </p>
      <div className={classes.actions}>
        <button type="button" onClick={cancelHandler} disabled={isSubmitting}>
          Cancel
        </button>
        <button disabled={isSubmitting}>
          {isSubmitting ? "Submitting..." : "Save"}
        </button>
      </div>
    </Form>
  );
}

export default EventForm;

export async function action({ request, params }) {
  const method = request.method;
  const data = await request.formData();
  const eventData = {
    title: data.get("title"),
    image: data.get("image"),
    date: data.get("date"),
    description: data.get("description"),
  };

  let url = "http://localhost:8080/events";

  if (method === "PATCH") {
    const eventID = params.eventID;
    url = "http://localhost:8080/events/" + eventID
  }

  const response = await fetch(url, {
    method: method,
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(eventData),
  });

  if (response.status === 422) {
    return response;
  }

  if (!response.ok) {
    throw json({ message: "Could not save the event" }, { status: 500 });
  }

  return redirect("/events");
}

```

Parent component to form:
```JSX
import { useRouteLoaderData } from 'react-router-dom'
import EventForm from '../components/EventForm'

function EditEventPage() {
    const data = useRouteLoaderData('event-detail');

    return (
        <EventForm method='patch' event={data.event} />
    )
}

export default EditEventPage
```

Routes:
```JSX
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import RootLayout from "./pages/Root";
import HomePage from "./pages/HomePage";
import EventsPage, { loader as eventsLoader } from "./pages/EventsPage";
import EventDetailPage, {
  loader as eventDetailsLoader,
  action as deleteEventAction
} from "./pages/EventDetailPage";
import NewEventPage from "./pages/NewEventPage";
import EditEventPage from "./pages/EditEventPage";
import EventsRootLayout from "./pages/EventsRoot";
import ErrorPage from "./pages/Error";
import {action as manipulateEventAction} from './components/EventForm'

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
                action: deleteEventAction
              },
              { path: "edit", action: manipulateEventAction , element: <EditEventPage /> },
            ],
          },

          { path: "new", action: manipulateEventAction,  element: <NewEventPage /> },
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