- Use React routes and create a logout page
- Wont contain a component
	- Only export function

```JS
import { redirect } from "react-router-dom";

export function action(){
    localStorage.removeItem('token');
    return redirect('/');
}
```

- register route

```JS
import {action as logoutAction} from './pages/Logout'

const router = createBrowserRouter([
	...
      {
        path: 'logout',
        action: logoutAction,
      },
```


# Logout user after token is expired

- Backend may be set to have token expire after a specified time

```JS
function createJSONToken(email) {
  return sign({ email }, KEY, { expiresIn: '1h' });
}
```

Have frontend remove the local storage

- Example approach
	- Use useEffect to start a timer whenever the token is changed and exists
	- Use useSubmit to post to the logout route

```JS
function RootLayout() {
  const token = useLoaderData();
  // const navigation = useNavigation();
  const submit = useSubmit();

  useEffect(() => {
    if (!token) {
      return;
    }

    if (token === "EXPIRED") {
      submit(null, { action: "/logout", method: "post" });
    }

    const tokenDuration = getTokenDuration();

    setTimeout(() => {
      submit(null, { action: "/logout", method: "post" });
    }, tokenDuration);
  }, [token]);
```

Util function:
```JS
export function getTokenDuration() {
  const StoredExpirationDate = localStorage.getItem("expiration");
  const expirationDate = new Date(StoredExpirationDate);
  const now = new Date();
  const duration = expirationDate.getTime() - now.getTime();
  return duration;
}

export function getAuthToken() {
  const token = localStorage.getItem("token");

  const tokenDuration = getTokenDuration();

  if (!token) {
    return null;
  }

  if (tokenDuration < 0) {
    return "EXPIRED";
  }

  return token;
}
```