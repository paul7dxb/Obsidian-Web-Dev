# Run Test

```bash
npm test
```

- Test will look for files with .test file extension and run the test

# Testing Component Events

Example. Checkbox change value:

Checkbox.js
```jsx
import { useReducer } from "react";

export function Checkbox() {

    const [checked, setChecked] = useReducer(
        (checked) => !checked,
        false
    );

    return (
        <>
        <label htmlFor="checked">
            {checked ? "checked" : "not checked"}
        </label>
        <input
        id="checked"
        type="checkbox" value={checked} onChange={setChecked} />
        </>
    )
}
```

Checkbox.test.js
``` js
import { Checkbox } from "./Checkbox";
import {fireEvent, render} from "@testing-library/react"

test("Selecting checkbox change value to true", () => {
    const {getByLabelText} = render(<Checkbox />);

    //Check that label has value not checked (use i for case insensitive)
    const checkbox = getByLabelText(/not checked/i);

    fireEvent.click(checkbox);
    expect(checkbox.checked).toEqual(true);

});
```

