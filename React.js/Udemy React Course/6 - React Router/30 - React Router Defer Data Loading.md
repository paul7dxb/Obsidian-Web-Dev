- Showing parts of a page while the rest of the data is found
- Render the component even though all the data isn't there yet

- Use the defer function from react-router-dom
- Used inside the loader function
- Takes an object
	- Pass object to defer that contains all HTTP requests
	- Promise from the executed function is accessed through the chosen key in the defer object

- In the component that uses the data
	- Return another component (the await component)
		- Resolve prop is one of the defered values
		- Between the Await component put a function that willl be executed once the data is there
- Wrap the await componentin the suspense component
	- Shows a fallback while the data is loaded


## Usage

```JSX
import { Suspense } from "react";
import { Await, defer, json, useLoaderData } from "react-router-dom";

import EventsList from "../components/EventsList";

function EventsPage() {
  const { events } = useLoaderData();

  return (
    <Suspense fallback={ <p style={{textAlign: 'center'}}>Loading... </p> } >
      <Await resolve={events}>  
        {(loadedEvents) => <EventsList events={loadedEvents} />}
      </Await>
    </Suspense>
  );
}

export default EventsPage;

// Defer function used to move to page and then display the data

async function loadEvents() {
  const response = await fetch("http://localhost:8080/events");

  if (!response.ok) {
    throw json({ message: "Could not fetch events" }, { status: 500 });
  } else {
	//response data needs to be handled properly
    const resData = await response.json()
    return resData.events;
  }
}

export function loader() {
  //Pass object to defer that contains all HTTP requests
  return defer({
    events: loadEvents(),
  });
}

```

# Split Solution

- Where you want to wait for one piece of data to be loaded before the page is rendered but then defer the loading of the other data which can be rendered on the page later
	- Use the await function on one of the defered items so react router knows when to load the page

- Ensure that lists with Links being rendered in multiple components use absolute links 

