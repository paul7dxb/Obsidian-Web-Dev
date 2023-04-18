- Tracking logged in status can be done by
	- Using context
	- Using react router
		- loader can be used to access state of data that will then be available to all child components
		- All pages that use the data from the loader will be updated when it changes

- Assign id to route holding the data so that it can be accessed

```JSX
const router = createBrowserRouter([
  {
    path: '/',
    element: <RootLayout />,
    errorElement: <ErrorPage />,
    id: 'root',
    loader : tokenLoader,
    children: [
```

util funciton
```JS
export function getAuthToken(){
    const token = localStorage.getItem('token');
    return token;
}

export function tokenLoader(){
    return getAuthToken();
}
```

Access in Component
```JSX
function MainNavigation() {
  const token = useRouteLoaderData('root')

  ...
          {!token && (
            <li>
              <NavLink
                to="/auth?mode=login"
                className={({ isActive }) =>
                  isActive ? classes.active : undefined
                }
              >
                Authentication
              </NavLink>
            </li>
          )}
          {token && (
            <li>
              <Form action="/logout" method="POST">
                <button>Logout</button>
              </Form>
            </li>
          )}
        </ul>
      </nav>
  
```

