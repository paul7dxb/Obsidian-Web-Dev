- Simple demo of a custom HTTP hook [[17 - Custom Hooks#HTTP Hook Example|here]]

# Example

- Example app found [on GitHub](https://github.com/paul7dxb/react-udemy-course/tree/master/react-custom-hooks-tasks-api-app)
- Structure

![[Image_React_Custom_Hook_API_Structure.png]]

use-http.js:
```JSX
import { useCallback, useState } from "react";

//requestConfig object contains url, method, headers, body
//applyData function handles the data that comes back from the request
//Assumes working with JSON data

const useHttp = () => {

    

  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const sendRequest = useCallback( async (requestConfig, applyData) => {
    setIsLoading(true);
    setError(null);
    try {
        //Check these parameters are set. If not set a default GET request
      const response = await fetch(
        requestConfig.url, {
            method: requestConfig.method ? requestConfig.method : 'GET',
            headers: requestConfig.headers ? requestConfig.headers : {},
            body: requestConfig.body ? JSON.stringify(requestConfig.body) : null
        }
      );

      if (!response.ok) {
        throw new Error("Request failed!");
      }

      const data = await response.json();

      applyData(data);

    } catch (err) {
      setError(err.message || "Something went wrong!");
    }
    setIsLoading(false);
  },[]);

  return {
    isLoading,
    error,
    sendRequest
  }
};

export default useHttp;

```

App.js (Get request maker):
```JSX
import React, { useEffect, useState } from "react";

import Tasks from "./components/Tasks/Tasks";
import NewTask from "./components/NewTask/NewTask";
import useHttp from "./hooks/use-http";

function App() {
  const [tasks, setTasks] = useState([]);

  //Destructure returned object to variables
  //Use alias for sendRequest to fetchTasks
  const { isLoading, error, sendRequest: fetchTasks } = useHttp();

  useEffect(() => {
    const transformTasks = (tasksObj) => {
      const loadedTasks = [];

      for (const taskKey in tasksObj) {
        loadedTasks.push({ id: taskKey, text: tasksObj[taskKey].text });
      }

      setTasks(loadedTasks);
    };

    fetchTasks(
      { url: "https://react-http-6a1db-default-rtdb.firebaseio.com/tasks.json" },
      transformTasks
    );
  }, [fetchTasks]);

  const taskAddHandler = (task) => {
    setTasks((prevTasks) => prevTasks.concat(task));
  };

  return (
    <React.Fragment>
      <NewTask onAddTask={taskAddHandler} />
      <Tasks
        items={tasks}
        loading={isLoading}
        error={error}
        onFetch={fetchTasks}
      />
    </React.Fragment>
  );
}

export default App;

```

NewTask.js (POST request maker from form data):
```JSX
import useHttp from "../../hooks/use-http";
import Section from "../UI/Section";
import TaskForm from "./TaskForm";

const NewTask = (props) => {
  const { isLoading, error, sendRequest: sendTaskRequest } = useHttp();

  const createTask = (taskText, taskData) => {
    const generatedId = taskData.name; // firebase-specific => "name" contains generated id
    const createdTask = { id: generatedId, text: taskText };

    props.onAddTask(createdTask);
  }

  const enterTaskHandler = async (taskText) => {
    sendTaskRequest({
      url: "https://react-http-6a1db-default-rtdb.firebaseio.com/tasks.json",
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: { text: taskText }
    }, createTask.bind(null, taskText)); //preconfiure function with bind .bind(this, 1st arg to bind). Other call binding still occurs appended after

  };

  return (
    <Section>
      <TaskForm onEnterTask={enterTaskHandler} loading={isLoading} />
      {error && <p>{error}</p>}
    </Section>
  );
};

export default NewTask;

```