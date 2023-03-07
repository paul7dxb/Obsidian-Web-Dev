
```JSX
import { json, redirect } from "react-router-dom";
import AuthForm from "../components/AuthForm";

function AuthenticationPage() {
  return <AuthForm />;
}

export default AuthenticationPage;

export async function action({ request, params }) {
  // Get mode
  const searchParams = new URL(request.url).searchParams;
  const mode = searchParams.get("mode") || "login";

  // Throw error if user entered a different url
  if (mode !== "login" && mode !== "signup") {
    throw json({ message: "Unsupported mode" }, { status: 422 });
  }

  // Get form data
  const data = await request.formData();
  const authData = {
    email: data.get("email"),
    password: data.get("password"),
  };

  // Send POST to backend
  const response = await fetch("http://localhost:8080/" + mode, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(authData),
  });

  // Check response
  if (response.status === 422 || response.status === 401) {
    return response;
  }
  if (!response.ok) {
    throw json(
      { message: "Could not authenticate the user." },
      { status: 500 }
    );
  }

  // Manage token

  // Redirect user
  return redirect('/')
}
```