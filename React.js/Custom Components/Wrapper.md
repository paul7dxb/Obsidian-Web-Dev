- Used to aviod "div soup" because of JSX requirement for one root element
- Same as the React.Fragment component

Wrapper.js
```JS
const Wrapper = props => {
    return props.children
};

export default Wrapper;
```

Component to render multiple:
```JSX
import Wrapper from "../Helper/wrapper";

  return (
	<Wrapper>
		<ComponentOne />
		<ComponentTwo />
		<ComponentThree />
	</Wrapper>
```

