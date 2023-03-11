- Allow you to make PAI endpoints as part of the projects

- Add api folder in the  pages folder

- Files will not contain components
- Define functions that define server side code
	- Only runs on the server
	- Triggered when request is made to the route

# Connect to DB

- Set up a database to connect to, e.g:
- [[MongoDB]]

## Call db interaction in app

### POST data to server

- Create handler for the request
- Use MongoClient

```JS
// /api/new-meetup
//  POST /api/new-meetup

import { MongoClient } from "mongodb";

async function handler(req, res) {
  if (req.method == "POST") {
    const data = req.body;
    const { title, image, address, description } = data;

    const client = await MongoClient.connect(
      "mongodb+srv://<username>:<password>@cluster0.fdlahzk.mongodb.net/<dbName>?retryWrites=true&w=majority"
    );

    //  Get db
    const db = client.db();
    const meetupsCollection = db.collection('meetups')

    // Insert full object as no requirement to use destructuring
    const result = await meetupsCollection.insertOne(data)
    console.log(result);

    // Close connection and send response to application
      client.close();
      res.status(201).json({message: 'Meetup inserted'})
  }
}

export default handler;

```

- Call handler for the POST request in application
	- Can use absolute path to go to anoter route on the server

```JSX
// domain.com/new-meetup

import NewMeetupForm from "@/components/meetups/NewMeetupForm";
import { useRouter } from "next/router";

function NewMeetupPage() {
  const router =  useRouter()
  
  async function addMeetupHandler(enteredMeetupData) {
    const response = await fetch("/api/new-meetup", {
      method: "POST",
      body: JSON.stringify(enteredMeetupData),
      headers: {
        "Content-Type": "application/json",
      },
    });

    const data = await response.json();
    console.log(data);

    // redirect user back to homepage after response
    router.push('/')
  }

  return <NewMeetupForm onAddMeetup={addMeetupHandler} />;
}

export default NewMeetupPage;

```

### Get  data from server

- Similar connection setup to POST
- Use find() method to get the data
- Needs to be processed properly
	- Map the data as the mongoDB data needs to be handled differently
	- take \_id and convert to string

# Static Props

```JS
export async function getStaticProps() {
  //fetch data from API

  const client = await MongoClient.connect(
      "mongodb+srv://<username>:<password>@cluster0.fdlahzk.mongodb.net/<dbName>?retryWrites=true&w=majority"
  );

  //  Get db
  const db = client.db();
  const meetupsCollection = db.collection('meetups')

  const meetups = await meetupsCollection.find().toArray();
  
  client.close();


  return {
    props: { meetups: meetups.map(meetup =>( {
      title: meetup.title,
      address: meetup.address,
      image: meetup.image,
      id: meetup._id.toString()
    })) },
    revalidate: 10,
  };
}
```

## Variable Path name

- When the route is variable use getStaticPaths to map out the required routes
```JS
export async function getStaticPaths() {
  const client = await MongoClient.connect(
      "mongodb+srv://<username>:<password>@cluster0.fdlahzk.mongodb.net/<dbName>?retryWrites=true&w=majority"
  );

  //  Get db
  const db = client.db();
  const meetupsCollection = db.collection("meetups");

  //find by param1: filter, param2: fields. Here only fetch IDs
  const meetups = await meetupsCollection.find({}, { _id: 1 }).toArray();

  client.close();

  return {
    fallback: false,
    // These paths would tyocally be made dynamically with a call to the database
    paths: meetups.map((meetup) => ({
      params: { meetupId: meetup._id.toString() },
    })),
  };
}
```

- Then use the route data to get the required info from the database

```JS
export async function getStaticProps(context) {
  // fetch API data for single meetup
  const meetupId = context.params.meetupId;

  const client = await MongoClient.connect(
      "mongodb+srv://<username>:<password>@cluster0.fdlahzk.mongodb.net/<dbName>?retryWrites=true&w=majority"
  );

  //  Get db
  const db = client.db();
  const meetupsCollection = db.collection("meetups");

  const selectedMeetup = await meetupsCollection.findOne({
    _id: new ObjectId(meetupId),
  });

  client.close();

  return {
    props: {
      meetupData: {
        id: selectedMeetup._id.toString(),
        title: selectedMeetup.title,
        address: selectedMeetup.address,
        image: selectedMeetup.image,
        description: selectedMeetup.description,
      },
    },
  };
}
```