
- Or withRouter in a class based component

# Using useRouter

- router.pathname
	- Path inferred by next(js)
		- /portfolio/\[projectid]
- router.query
	- Object with dynamic content part

# useRouter Usage

```JS
//For structure /portfolio/[projectid]
//Navigate to /portfolio/something

import { useRouter } from "next/router";

const PortfolioPorjectPage = () => {
	const router = useRouter();

    router.pathname 
	console.log(router.pathname) // /portfolio/[projectid]
    router.query
	console.log(router.query) // {projectid: "something"}

...

```


![[NextJS_useRouter_Properties.png]]


# Catch All Routes With Slug

- Example case urls to get to a blog post
	- Want to be able to get to post from
		- blog/postID
		- blog/2022-12/postid
		- blog/someQuery/postid


![[NextJS_Slug.png]]

- When accessing router.query the object will contain slug (or used name in structure) containing an array of parameters in order

- If there is another dynamic route at the slug level the slug will not kick in until there is more than on element to the route

![[Next_JS_Slug_Multiple.png]]
# Programatic Routes

- Example submitting a form
- Use the push or replace property from useRouter

```JSX
import {useRouter} from "next/router"

const ClientsProjectsPage = () => {
    const router = useRouter()
    const clientID = router.query.clientid
    console.log(clientID)

    const loadProjectHandler = () => {
        // Function work e.g loading data

        // Navigate to different page
        // router.replace('/clients/max/projectA') // Replace would prevent navigating back from next page
        // router.push('/clients/max/projectA')
        router.push({pathname: '/clients/[clientid]/[clientprojectid]', query: {clientid: clientID, clientprojectid: "Project A" } })
    }

    return (
        <div>
            <h1>The Projects from a Given Client</h1>
            <button onClick={loadProjectHandler}>Programatic Navigation to Project A</button>
        </div>
    )
}

export default ClientsProjectsPage
```