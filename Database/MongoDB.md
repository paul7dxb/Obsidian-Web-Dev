- NoSQL database
- Works with collections of documents
	- collections = tables
	- documents = entries

- Create cluster
- Add IP to allowed connection
- Create user that can read and write to DB
- Choose connection method from sections below

NEVER run on client side, use API calls

# NextJS

## Save Data to DB

- Choose connection method from sections below
	- Connect application
	- Choose nextjs
	- Copy connection string

Install mongoDB drvier in project
```bash
npm install mongodb
```

- Connect to cluster and insert driver in application
- Returns a promise so we can use async await
- If database doesnt exitst it will be created

- Now [[6 - API routes#Call db interaction in app|use db in application]]

## Get data from DB

- NextJS allows fetch call on serverside (usually only availbale in browser)

# Working with Object IDs

- MongoDB uses objects for the ids which need to be converted to work as strings in application

## object to string


## string to MongoDB object

```JS
import { MongoClient, ObjectId } from "mongodb";

export async function getStaticProps(context) {
  // fetch API data for single meetup
  const meetupId = context.params.meetupId;

	// DB access code

  const selectedMeetup = await meetupsCollection.findOne({
    _id: new ObjectId(meetupId),
  });

  return {
    props: {
      meetupData: {
		...
      }, },};
}
```