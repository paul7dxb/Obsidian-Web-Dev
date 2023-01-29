- Use spread operator to keep input usage general / highly configurable and send in value via props
	- e.g type: text

```JSX
import React from 'react'
import classes from './Input.module.css'

const Input = (props) => {
    return(
        <div className={classes.input}>
            <label htmlFor={props.input.id}>{props.label}</label>
            <input {...props.input} />
        </div>
    ) 
}

export default Input
```

- ID is included in the props so id is assigned to input
- props.input is expected to be an object

## Usage in Parent