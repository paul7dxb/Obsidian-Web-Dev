# Use Cases

- Form In Other Routes
	- Example a sign up form
	- This form can be shown in almost all routes so you do not want to use tbe normal submission action as it calls the closest action
- Behind the scenes actions
	- Interacting with an action or loader without triggering a route change

## Why It Is Required

- Issue using 'action' attribute:
- Can call the action by using the 'action' attribute on the form to target a single route
	- This would initialise a transition to the route

## Resolution

- Use the hook - useFetcher()
	- Contains different form/submit
	- Difference is that the action is performed but does not perform a route transition
	- Prevents navigation to where the action belongs
		- Example: Trigger the action of the /newsletter route to sign up

# Usage

- use useFetcher.Form in the form component
	- Get access to the data and state from the fetcher object
- Use useEffect to rerender when there is a change in state  for the useFetcher action

Form component:
```JSX
import { useEffect } from "react";
import { useFetcher } from "react-router-dom";
import classes from "./NewsletterSignup.module.css";

function NewsletterSignup() {
  const fetcher = useFetcher();
  const { data, state } = fetcher;

  useEffect(() => {
    if (state === "idle" && data && data.message) {
      window.alert(data.message);
    }
  }, [data, state]);

  return (
    <fetcher.Form method="post" action="/newsletter" className={classes.newsletter}>
      <input
        type="email"
        placeholder="Sign up for newsletter..."
        aria-label="Sign up for newsletter"
      />
      <button>Sign up</button>
    </fetcher.Form>
  );
}

export default NewsletterSignup;

```

Parent Action component:
```JSX
import NewsletterSignup from '../components/NewsletterSignup';
import PageContent from '../components/PageContent';

function NewsletterPage() {
  return (
    <PageContent title="Join our awesome newsletter!">
      <NewsletterSignup />
    </PageContent>
  );
}

export default NewsletterPage;

export async function action({ request }) {
  const data = await request.formData();
  const email = data.get('email');

  // send to backend newsletter server ...
  console.log(email);
  return { message: 'Signup successful!' };
}
```

Main Navigation bar that includes sign up rendered in rootLayout:
```JSX
import { NavLink } from 'react-router-dom';

import classes from './MainNavigation.module.css';
import NewsletterSignup from './NewsletterSignup';

function MainNavigation() {
  return (
    <header className={classes.header}>
      <nav>

			...
			
      </nav>
      <NewsletterSignup />
    </header>
  );
}

export default MainNavigation;

```


Routes:
```JSX
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import RootLayout from "./pages/Root";
import NewsletterPage, { action as newsletterAction } from './pages/Newsletter';

//Create router

const router = createBrowserRouter([
  {
    path: '/',
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    children: [
      { index: true, element: <HomePage /> },
      {
			...
      },
      {
        path: 'newsletter',
        element: <NewsletterPage />,
        action: newsletterAction,
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```