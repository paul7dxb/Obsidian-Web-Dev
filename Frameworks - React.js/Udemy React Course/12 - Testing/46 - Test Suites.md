- One feature or one Component
- Using global describe() function
	- Two args (description, function holding the test functions for that suite )

# Example Test Suite for a simple component

Component Greeting.js:
```JSX
import { useState } from "react"


const Greeting = () => {
    const [changedText, setChangedText] = useState(false)

    const changeTextHandler = () => {
        setChangedText(true)
    }

    return (
        <div>
            <h2>Hello World!</h2>
            {!changedText && <p>It's good to see you!</p>}
            {changedText && <p>Changed!</p>}
            <button onClick={changeTextHandler}>Change Text</button>
        </div>
    )
}

export default Greeting
```

Test Suite:
Greeting.test.js
```JS
import { render, screen } from "@testing-library/react";
import Greeting from "./Greeting";
import userEvent from '@testing-library/user-event'

describe("Greeting component", () => {
  test("renders hello world as a text", () => {
    //Arrange
    render(<Greeting />);

    // Act
    // ...Nothing

    // Assert
    // Case insensitive or substrings with exact: false
    const helloWorldElement = screen.getByText("Hello World", { exact: false });
    expect(helloWorldElement).toBeInTheDocument();
  });

  test("renders 'It's good to see you!' if button not clicked", () => {
    //Arrange
    render(<Greeting />);

    // Act
    // ...Nothing

    // Assert
    // Case insensitive or substrings with exact: false
    const seeYouElement = screen.getByText("It's good to see you!", { exact: false });
    expect(seeYouElement).toBeInTheDocument();
  });



  test("renders 'Changed' as a text if button is clicked", () => {
    //Arrange
    render(<Greeting />);

    // Act
    // Click the button
    const buttonElement = screen.getByRole("button")
    userEvent.click(buttonElement)

    // Assert
    // Case insensitive or substrings with exact: false
    const outputElement = screen.getByText("Changed", { exact: false });
    expect(outputElement).toBeInTheDocument();
  });

  test("does not render 'It's good to see you!' is not visible if button clicked", () => {
    //Arrange
    render(<Greeting />);

    // Act
    // Click the button
    const buttonElement = screen.getByRole("button")
    userEvent.click(buttonElement)

    // Assert
    // Use query to not throw error on not finding. Expect not to be visible
    const seeYouElement = screen.queryByText("It's good to see you!", { exact: false });
    expect(seeYouElement).not.toBeInTheDocument();
  });

});

```