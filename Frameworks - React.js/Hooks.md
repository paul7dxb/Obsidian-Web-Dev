## useSearchParams()
- Get the query parameters from the url
- [[34 - Query Parameters|Query Parameters with useSearchParams]]

## useActionData()

- Get response data
- Useful for getting error messages
- Examples:
	- [[36 - Validation Errors|Authentication Error Response]]

## useNavigation()

- Track current navigation state
	- Submitting
	- Idle
	- Loading
- Examples:
	- [[36 - Validation Errors|Disable Button When Submitting Form]]

## useLoaderData()

- React-router hook
- Get access to data from loader function defined in route declaration
	- For children to get access use useRouteLoaderData('parentRoute')

## useSubmit()

- Programmatically submit a form

## useRef()

- Often used in forms where two way binding is not needed
- [[2 - Hooks#useRef Hook|useRef notes]]