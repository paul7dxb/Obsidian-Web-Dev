


- State Management System or cross component or app wide state
- Only ever have **ONE** store
	- Central Data (State) Store

- Components subscribe to the store to get a "silce" of the store
- Components NEVER directly manipulate the store data

![[Image_React_Redux_Process.png]]

- Reducer function is responsible for mutating thstore data
	- Not a useReducer hook
	- Take input and transform input to create a new output (a general programming concept)

- Components dispath (trigger) Actions
	- Redux forwards actions to reducer
	- Reads type of operration
	- Reducer performs operation
	- Reducer spits out a new state
	- Relevant components notified of update