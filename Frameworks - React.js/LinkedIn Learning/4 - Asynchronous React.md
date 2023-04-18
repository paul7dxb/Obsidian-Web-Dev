Fethc data using useEffect and useState

```JSX
function GitHubUser({ name, pubRepos, avatar }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{pubRepos}</p>
      <img src={avatar} height={150} alt="github avatar" />
    </div>
  );
}

function App() {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(`https://api.github.com/users/paul7dxb`)
      .then((response) => response.json())
      .then(setData);
  }, []);

  if (data)
    return (
      <GitHubUser
        name={data.login}
        pubRepos={data.public_repos}
        avatar={data.avatar_url}
      />
    );

  return <h1>Data</h1>;
}
```

Loading state: fetching in progress

# useState For Flow of data

use multiple useStates to process data loading

```JSX
import { useEffect, useState } from "react";

function GitHubUser({ name, pubRepos, avatar }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{pubRepos}</p>
      <img src={avatar} height={150} alt="github avatar" />
    </div>
  );
}

function App() {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    fetch(`https://api.github.com/users/paul7dxb`)
      .then((response) => response.json())
      .then(setData)
      .then(() => setLoading(false))
      .catch(setError);
  }, []);

  if (loading) return <h1>Loading...</h1>
  if (error) return <pre>{JSON.stringify(error)}</pre>
  if (!data) return null;
    return (
      <GitHubUser
        name={data.login}
        pubRepos={data.public_repos}
        avatar={data.avatar_url}
      />
    );

}
```