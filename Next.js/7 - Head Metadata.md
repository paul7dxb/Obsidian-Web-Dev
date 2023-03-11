- Metadata for the head section
	- Description meta tag
		- Shows up in the google search
	- Page title

# Head Component

```JSX
import Head from "next/head";

function HomePage(props) {
  return (
    <>
      <Head>
        <title>React Meetups</title>
        <meta
          name="description"
          content="Browse a list of active React Meetups"
        />
      </Head>
      <MeetupList meetups={props.meetups} />;
    </>
  );
}
```

- variable metadata

```JSX
function MeetupDetails(props) {
  return (
    <>
      <Head>
        <title>{props.meetupdata.title}</title>
        <meta name="description" content={props.meetupData.description} />
      </Head>
      <MeetupDetail
        image={props.meetupData.image}
        title={props.meetupData.title}
        address={props.meetupData.address}
        description={props.meetupData.description}
      />
    </>
  );
}
```