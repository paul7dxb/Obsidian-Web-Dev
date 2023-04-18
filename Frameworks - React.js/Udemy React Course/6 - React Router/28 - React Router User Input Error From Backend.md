- If the backend responds to a submission with an error code you will want to remain on that same page instead of redirecting away
- return the data instead of throwing the error

- Use the returned action data in the component
	- useActionData
		- Gives access returned by closest action

# Usage

- In action function check for the error (e.g 422)
- In form component use the hook useActionData to get the response

```JS
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

  if (response.status === 422){
    return response;
  }
  
	...
	
```

form:
```JSX
import { useNavigate, useNavigation, useActionData } from "react-router-dom";
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
    <Form method="post" className={classes.form}>
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
		...
		
    </Form>
  );
}

export default EventForm;

```