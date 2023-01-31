
# Use

- Follow rule for funciton name in file
	- Function must start with use
		- Tells React it will be a custom hook
		- Respecting use of hooks
	- See example below
- Any states in the custom hoook will be tied to the component that calls it
	- Not shared between components that use the custom hook
	- Just the logic is shared, not the concrete state
- You can return states from the custom hook back to the calling component

# Where to Store

![[Image_React_Custom_Hooks_Directory.png]]

- Create a hooks folder under src

# Example

- Example code:
	- https://github.com/paul7dxb/react-udemy-course/tree/master/react-custom-hooks

- import custom hook
- Call the custom hook function

Custom Hook:
use-counter.js:
```JS
import { useEffect, useState } from "react";

const useCounter = (forwards = true) => {
    const [counter, setCounter] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
        if(forwards){
            setCounter((prevCounter) => prevCounter + 1);
        } else {
            setCounter((prevCounter) => prevCounter - 1);
        }  
    }, 1000);

    return () => clearInterval(interval);
  }, [forwards]);

  return counter;
};

export default useCounter;
```

Using in a component:
ForwardCounter.js:
```JSX
import useCounter from '../hooks/use-counter';
import Card from './Card';

const ForwardCounter = () => {
const counter = useCounter(true);
  return <Card>{counter}</Card>;
};

export default ForwardCounter;
```