- File based routing instead of code based routing in React
- Can handle static and Dynamic routes

# Setup

- Use special /pages folder to infer structure
- Route files will contain regular React component

- Routes:
	- index.js is assumed to be root path
	- Other paths are the name of the route
	- Square brackets for dynamic routes
		- Can be on a file or folder (for nested dynamic structure)

![[Next_JS_Routes.png.png]]
![[NextJS_Route_Structure_VSCode.png]]



# Accessing URL Data

- Use the [[useRouter]] hook
- For Catch all routes use [[useRouter#Catch All Routes With Slug|Slug structure]]


# NextJS Links

- Using a tags will send new HTTP request. This will lose app state
	- Get brand new HTML page losing app state
- Hovering over a Link will start to prefetch data
- Replace prop will prevent being able to go back

```JSX
import Link from "next/link";

const HomePage = () => {
	return (
		<div>
			<h1>The Home Page</h1>
			<ul>
				<li>
					<Link href="/portfolio">Portfolio</Link>
				</li>
				<li>
			...
```

## Navigate to Dynamic Routes

- Can use template literals or an object
```JSX
import Link from "next/link";

const ClientsPage = () => {
	const clients = [
		{ id: "paul", name: "Paul" },
		{ id: "max", name: "Max" },
	];
	return (
		<div>
			<h1>The Clients Page</h1>
			<ul>
				<li>
					{clients.map((client) => (
						<li id={client.id}>
                            {/* Access by literal */}
							{/* <Link href={`/clients/${client.id}`}>  */}
							<Link
                            // Access by object
								href={{
									pathname: "/clients/[id]",
									query: { id: client.id },
								}}
							>
								{client.name}
							</Link>
						</li>
					))}
				</li>
			</ul>
		</div>
	);
};

export default ClientsPage;



```

- Using an object
	- pathname: As it is in the Project directory
		- pathname: '/clients/\[id]'
	- query: Give the query parameters to fill in the pathname
		- query: { id: client.id }

# Programatic Routes

- Example submitting a form
- Use the push or replace property from [[useRouter]]

# 404  Page

- Add '404.js' to pages
- Create page as a normal component

\<evce>


# \_app.js

- Root component
- Wraps page components