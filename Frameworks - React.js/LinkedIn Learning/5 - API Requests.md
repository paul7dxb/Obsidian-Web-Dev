```JSX
import { useEffect, useState } from "react";

//Query to make to API
const query = `query {
  allLifts{
    name
    elevationGain
    status
  }
}`;

//Options for API request with query added in
const opts = {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ query }),
};

function Lift({ name, elevationGain, status }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>
        {elevationGain} {status}
      </p>
    </div>
  );
}

function App() {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true);
    //Make fetch request with the options set
    fetch(`http://snowtooth.moonhighway.com/`, opts)
      .then((response) => response.json())
      .then(setData)
      .then(() => setLoading(false))
      .catch(setError);
  }, []);

  //Deal with loading stage
  if (loading) return <h1>Loading...</h1>;
  if (error) return <pre>{JSON.stringify(error)}</pre>;
  if (!data) return null;
  return (
    <div>
      {data.data.allLifts.map((lift) => (
        <Lift
          name={lift.name}
          elevation={lift.elevation}
          status={lift.status}
        />
      ))}
    </div>
  );
}
```