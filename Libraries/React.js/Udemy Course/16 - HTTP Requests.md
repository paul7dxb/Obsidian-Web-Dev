- Used to fetch data from database

# Principle

- Access database via backend machine
	- Backend written in whatever language

# Fetch API

- Fetch and send data
- Send HTTP requests and work with responses

# Example

## .then()

```JS
  const [movies, setMovies] = useState([]);


  function fetchMoviesHandler(){
    fetch('https://swapi.dev/api/films').then((response) => {
      return response.json();
    }).then((data) => {
      const transformedMovies = data.results.map((movieData) => {return {id: movieData.episode_id, title: movieData.title, openingText: movieData.opening_crawl, releaseData: movieData.release_date}})
      setMovies(transformedMovies)
    })
  }
```

## Async / await

```JS
  async function fetchMoviesHandler(){
    const response = await fetch('https://swapi.dev/api/films');
    const data = await response.json();
      const transformedMovies = data.results.map((movieData) => {
        return {id: movieData.episode_id, title: movieData.title, openingText: movieData.opening_crawl, releaseData: movieData.release_date}
      });
      setMovies(transformedMovies);
  }
```

## Performing the Async function on load

- Uses [[13 - useCallback()|useCallback()]] and [[7 - useEffect()|useEffect()]]

```JS
  const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch('https://react-http-6a1db-default-rtdb.firebaseio.com/movies.json');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

       const transformedMovies = data.results.map((movieData) => {
         return {
           id: movieData.episode_id,
           title: movieData.title,
           openingText: movieData.opening_crawl,
           releaseDate: movieData.release_date,
         };
       });
      setMovies(loadedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }, []);
  
  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);
```

# Loading Screen

- Use a useState for holding "isLoading"
- Change from false to true when loading function called
- Use conditionals in the JSX to show relevant data

```JSX
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);

  async function fetchMoviesHandler() {
    setIsLoading(true);
    const response = await fetch("https://swapi.dev/api/films");
    const data = await response.json();
    const transformedMovies = data.results.map((movieData) => {
      return {
        id: movieData.episode_id,
        title: movieData.title,
        openingText: movieData.opening_crawl,
        releaseData: movieData.release_date,
      };
    });
    setMovies(transformedMovies);
    setIsLoading(false);
  }

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>
        {!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
        {!isLoading && movies.length == 0 && <p>Found no movies</p>}
        {isLoading && <p>Loading...</p>}
      </section>
    </React.Fragment>
  );
}
```

# HTTP Error Status codes

- Handle HTTP status codes other than 200
- Responses other than 200 are technically not errors so will not throw error automatically
- Can use [[#Axios]] to handle status codes, or manually like example below:


```JSX
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  async function fetchMoviesHandler() {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch("https://swapi.dev/api/films");
      if (!response.ok) {
        throw new Error("Something went wrong");
      }
      const data = await response.json();

      const transformedMovies = data.results.map((movieData) => {
        return {
          id: movieData.episode_id,
          title: movieData.title,
          openingText: movieData.opening_crawl,
          releaseData: movieData.release_date,
        };
      });
      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>
        {!isLoading && movies.length > 0 && <MoviesList movies={movies} />}
        {!isLoading && movies.length == 0 && !error && <p>Found no movies</p>}
        {!isLoading && error && <p>{error}</p>}
        {isLoading && <p>Loading...</p>}
      </section>
    </React.Fragment>
  );
}
```

# Start Fetching by useEffect()

- [[7 - useEffect()#useEffect()|useEffect notes]]
- When request should be made as part of render cycle but not necessarily on every update to the component
- Use pointer to function as a dependency for when external elements are in the function (e.g a changing url for the API call)
	- To avoid rerender losing the function pointer use [[13 - useCallback()|useCallback()]]

```JS
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch("https://swapi.dev/api/films");
      if (!response.ok) {
        throw new Error("Something went wrong");
      }
      const data = await response.json();

      const transformedMovies = data.results.map((movieData) => {
        return {
          id: movieData.episode_id,
          title: movieData.title,
          openingText: movieData.opening_crawl,
          releaseData: movieData.release_date,
        };
      });
      setMovies(transformedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  },[]
  )

  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);

  let content = <p>Found no movies</p>

	//Conditionals to set content to other HTML

  return (
    <React.Fragment>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>
        {content}
      </section>
    </React.Fragment>
  );
}
```


# POST requests

- Can still use fetch, but need to set method to POST
- May need to handle responses


```JSX
function App() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const fetchMoviesHandler = useCallback(async () => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch('https://react-http-6a1db-default-rtdb.firebaseio.com/movies.json');
      if (!response.ok) {
        throw new Error('Something went wrong!');
      }

      const data = await response.json();

      const loadedMovies = [];

      for (const key in data){
        loadedMovies.push({
          id: key,
          title: data[key].title,
          openingText: data[key].openingText,
          releaseData: data[key].releaseData
        })
      }

      setMovies(loadedMovies);
    } catch (error) {
      setError(error.message);
    }
    setIsLoading(false);
  }, []);

  useEffect(() => {
    fetchMoviesHandler();
  }, [fetchMoviesHandler]);

  async function addMovieHandler(movie) {
    const response = await fetch('https://react-http-6a1db-default-rtdb.firebaseio.com/movies.json', {
      method: 'POST',
      body: JSON.stringify(movie),
      headers: {
        'Content-Type': 'application/json'
      }
    });
    const data = await response.json();
    console.log(data)
  }

  let content = <p>Found no movies.</p>;

  if (movies.length > 0) {
    content = <MoviesList movies={movies} />;
  }

  if (error) {
    content = <p>{error}</p>;
  }

  if (isLoading) {
    content = <p>Loading...</p>;
  }

  return (
    <React.Fragment>
      <section>
        <AddMovie onAddMovie={addMovieHandler} />
      </section>
      <section>
        <button onClick={fetchMoviesHandler}>Fetch Movies</button>
      </section>
      <section>{content}</section>
    </React.Fragment>
  );
}
```


# Useful libraries

## Axios
- JS library
- Makes sending and dealing with HTTP requests simple
- Able to throw errors for request error status codes