- In react router if an error is thrown react router will render the closest error element
	- Found with errorElement

In child component:
```JS
  if (!response.ok) {
    console.log("error")
    throw {message: "couldn't load data"}
```

In router:
```JS
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
          ...
```

## useRouteError() hook

- Allows you to access the errors that have been thrown
	- Thrown error, response or any other thrown data can be accessed

- Throwing responses with status codes
- Can access status code of thrown reponse through status property
	- Helps build

Example:
```JS
  if (!response.ok) {
    throw new Response(JSON.stringify({ message: "Could not fetch events" }), {
      status: 500,
    });
  } else {
```

```JS
import { useRouteError } from "react-router-dom";
import PageContent from "../components/PageContent";

function ErrorPage() {
  const error = useRouteError();

  let title = "An error occured";
  let message = "Something went wrong";

  if (error.status === 500) {
    message = JSON.parse(error.data).message;
  }
  if (error.status === 404) {
    title = "Not found"
    message = "Could not find page";
  }
  
  return (
    <PageContent title={title}>
      <p>{message}</p>
    </PageContent>
  );
}
```

# Using the react router JSON function

- A react router function that creates a new Response that includes data in the JSON format
	- Benifit is that when the data is then received it does not have to be parsed by the component
	- Parsing is done by react router

- Theo following is equivalent

```JS
import { json } from "react-router-dom";

throw new Response(JSON.stringify({ message: "Could not fetch events" }), {
      status: 500,
    });
throw json({ message: "Could not fetch events" }, { status: 500 });
```