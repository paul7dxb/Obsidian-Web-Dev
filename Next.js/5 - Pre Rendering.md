- useEffect will not execute until component function is complete
- This means in page source data from an API call using useEffect will not show
	- Rendered in second render

# Data Fetching for Static Pages

![[NextJS_Pre_Rendering.png]]

- static generation
	- Pre rendered at build time
	- Does not change after build
	- Changes require rebuiild and deploy

## getStaticProps()

- In pages can export a function getStaticProps()
	- A reserved name
	- Will execute function during pre rendering function
	- Allowed to be asyncronous
	- Allows pre rendering with required data
	- Code in here NEVER ends up client side
	- Must return an object
		- Usually return a props

Example with useEffect():
- Will not show in source code for pre rendering
```JSX
function HomePage(props) {
  const [loadedMeetups, setLoadedMeetups] = useState([]);
  useEffect(() => {
// send request and fetch data
setLoadedMeetups(DUMMY_MEETUPS) //simulated data geting
  },[])
  return <MeetupList meetups={loadedMeetups} />;
}
```

Using getStaticProps
```JSX
import MeetupList from "@/components/meetups/MeetupList";

const DUMMY_MEETUPS = [
  {
    id: "m1",
    title: "A First Meetup",
    image:
      "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Stadtbild_M%C3%BCnchen.jpg/1280px-Stadtbild_M%C3%BCnchen.jpg",
    address: "Some address 5, 12345 Some City",
    description: "This is a first meetup!",
  },
  {
    id: "m2",
    title: "A Second Meetup",
    image:
      "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Stadtbild_M%C3%BCnchen.jpg/1280px-Stadtbild_M%C3%BCnchen.jpg",
    address: "Some address 10, 12345 Some City",
    description: "This is a second meetup!",
  },
];

function HomePage(props) {
  return <MeetupList meetups={props.meetups} />;
}

export async function getStaticProps() {
  //fetch data from API
  return{props:{meetups: DUMMY_MEETUPS}}
}

export default HomePage;
```

# Incremental Static Generation

- Allows for re pre generation of content
- Number of seconds that will be waited between rerender
- Requires a request to be made to trigger the regeneration
- Use the revalidate property

## getStaticProps()

```JS
export async function getStaticProps() {
  //fetch data from API
  return {
    props: { meetups: DUMMY_MEETUPS },
    revalidate: 1,
  };
}
```

- Accessing url in function
	- Use the context.params
	- object where identifiers are properties and values are those encoded in the url
		- Encoded values are those in square brackets of the route
		

## getStaticPaths()

- Required in a page that is using a dynamic value in its path and also using getStaticProps()
	- This is becuase nextjs pregenerates all versions of a page during build
	- If user enters url for non pregenerated route they will get a 404 error
	- return object that describes all segment values that page should be pregenerated
- Array of objects per version of page
- Requires fallback key to know wether paths will have all supported id values
	- Anything else gets 404
	- fallback true will try to generate a dynamic content when request made
	- Pre generate common/popular or expected ones and let others be generated

```JS
export async function getStaticPaths() {
  return {
    fallback:false,
    // These paths would tyocally be made dynamically with a call to the database
    paths: [
      {
        params: {
          meetupId: "m1",
        },
      },
      {
        params: {
          meetupId: "m1",
        },
      },
    ],
  };
}
```

# Server Side Pre Render For Every Call

- getServerSideProps()
- Not run during build but on server after deployment
- Return object with props property
- Always ran on the server side
- Can run with credentials

- Requires user to have to wait for pre render on every request
- Better to use getStaticProps unless need access to concrete object and multiple changes per second
