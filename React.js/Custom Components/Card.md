[[1 - Components#Use Custom Component as Wrapper]]

Card.js:
```JSX
import React from "react";
import styles from "./Card.module.css";

const Card = (props) => {
  const classes = styles.card + props.className;
  return (
    <div className={`${styles.card} ${props.className} `}>{props.children}</div>
  );
};

export default Card;
```

Card.module.css:
```css
.card{
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 10px 6vw;
    background-color: bisque;
    padding: 10px;
}
```

## Usage:

- Example project:
	- [Udemy React Create User](https://github.com/paul7dxb/react-udemy-course/tree/master/react-create-user-app)
```JSX
import Card from "../UI/Card";

...

return (
	<Card className="input">
		...
	</Card>
```

