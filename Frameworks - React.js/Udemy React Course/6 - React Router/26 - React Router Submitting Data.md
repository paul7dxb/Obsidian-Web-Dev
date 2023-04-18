- React Router dom has its own Form component
- Prevents browser default submission
	- Gives the submission to the action instead of submitting to the backend when using the react-router-dom Form component
- Loader function gets sent to the action

- Loader function receives object that contains request and params properties

# Usage

- Set up action that receives a function in the route definitions
- Create POST function in component with loader function that sends the form data
	- Form data accessed from form using the react-router-dom Form component
- Access form data in loader function via the request parameters
- Create POST fetch request to send the data


Routes:
```JSX
import NewEventPage, {action as newEventAction} from "./pages/NewEventPage";

{ path: "new", action: newEventAction,  element: <NewEventPage /> },
```

NewEventPage.js:
```JSX
import { json, redirect } from "react-router-dom";
import EventForm from "../components/EventForm";

function NewEventPage() {
  return <EventForm />;
}

export default NewEventPage;

export async function action({request, params}) {
  const data = await request.formData();
  const eventData = {
    title: data.get('title'),
    image: data.get('image'),
    date: data.get('date'),
    description: data.get('description'),
  };
  const response = await fetch('http://localhost:8080/events', {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(eventData),
  });

  if (!response.ok) {
    throw json({ message: "Could not save the event" }, { status: 500 });
  }

  return redirect("/events");
}

```

EventForm:
```JSX
import { useNavigate } from "react-router-dom";
import { Form } from "react-router-dom";

import classes from "./EventForm.module.css";

function EventForm({ method, event }) {
  const navigate = useNavigate();
  function cancelHandler() {
    navigate("..");
  }

  return (
    <Form method='post' className={classes.form}>
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
          defaultValue={event ? event.data : ""}
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
        <button type="button" onClick={cancelHandler}>
          Cancel
        </button>
        <button>Save</button>
      </div>
    </Form>
  );
}

export default EventForm;

```

# Submitting to another path

- in the React-Router-Dom's Form properties set the `action="any-other-path"`

# Submite Data Programatically

- useSubmit() hook from react-router-dom
	- First argument is data to submit
	- Second argument are the same values as Form
		- `method: 'delete' , action, 'path'`

- Configure request to a delete request using passed in parameters

component Starting deletion:
```JS
import { Link, useSubmit } from "react-router-dom";
import classes from "./EventItem.module.css";

function EventItem({ event }) {
  const submit = useSubmit();

  function startDeleteHandler() {
    const proceed = window.confirm("Are you sure?");
    if (proceed) {
      submit(null, { method: "delete" });
    }
  }

```

Loader:
```JS
export async function action({params, request}){
const eventID=params.eventID;
const response = await fetch('http://localhost:8080/events/' +eventID, {
  method: request.method
});

if(!response.ok){
  throw json(
    {message: 'Could not delete the event'}, {status: 500}
  )
}
return redirect('/events')
}
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
import NewEventPage, {action as newEventAction} from "./pages/NewEventPage";
import EditEventPage from "./pages/EditEventPage";
import EventsRootLayout from "./pages/EventsRoot";
import ErrorPage from "./pages/Error";

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
              { path: "edit", element: <EditEventPage /> },
            ],
          },

          { path: "new", action: newEventAction,  element: <NewEventPage /> },
          ...
          
```

# UI for data submissions

- useNavigation() hook
	- Can find out state of the currently active transition is
	- Form submission creates transition
	- Can check if action has been complete

```JSX
import { useNavigation } from "react-router-dom";

function EventForm({ method, event }) {

  const navigation = useNavigation();
  const isSubmitting = navigation.state === "submitting";

  return (
    <Form method="post" className={classes.form}>
    
		...

      <div className={classes.actions}>
        <button type="button" onClick={cancelHandler} disabled={isSubmitting}>
          Cancel
        </button>
        <button disabled={isSubmitting}>
          {isSubmitting ? "Submitting..." : "Save"}
        </button>
      </div>
    </Form>
```