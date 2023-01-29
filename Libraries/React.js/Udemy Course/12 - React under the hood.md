
# State Change Render Component

- When a state is changed the component it sits in is re rendered
- This also rerenders ALL child components even if all its props (even if there are no props) don't change
- You can use react.memo but this is only recommended when there is a noticable performance drop
	- Checks if its props values have changed
	- If they have not the re rendering for this component is skipped
		- This also skips rerendering of child components
	- If rerendered component has a function the function reference will be new in passed down props as the function (although may have the same code) is not the same one
- This optimisation comes at a cost (needs to store and compare prop values)
	- Performance cost of comparison vs rerendering

# React Memo

- Used to prevent re evaluation that isn't neccessary

```JS
export default React.memo(ComponentName);
```

- When passing function references in props [[13 - useCallback()]] is needed to keep the function on re render preventing the reference needing to change

# State

## State Rendering

- State hooks links components and state
- Hooks get attached to components which React manages
- Why don't hooks get re initialised on re render?
	- First conponent render will create a new useState variable
	- React knows which components it will belong to and defualt value
	- subsequent render calls
		- No new state is created as React recongnises the old state used
		- React will update that state as needed

## State Updates & Scheduling

![[Image_React_State_Updates.png]]

- When set function is called React schedules a State update
	- Not carried out straight away
	- Performance intensive tasks may take priority and postpone change
- Order is kept for state change
	- Order of changes for same state change are performed in order
	- This is why it is important to work on most recent state using a function
		- [[2 - States#Updating State that depends on Previous State|Updating state dependent on previous state]]
		- useEffect will rerun for each state change as another solution to this problem
- Scheduling may also batch updates together before re render
	- E.g two state updating functions on consecutive lines