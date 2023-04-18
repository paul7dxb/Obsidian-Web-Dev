# Make a test

- Name test file after component
- Place test file as close to component file as possible
- Group together tests into [[46 - Test Suites|Test suites]]

Greeting.test.js
```JSX
import { render, screen } from "@testing-library/react"
import Greeting from "./Greeting"

test('renders hello world as a text', () => {
    //Arrange
    render(<Greeting/>)

    // Act
    // ...Nothing

    // Assert
    // Case insensitive or substrings with exact: false
    const helloWorldElement = screen.getByText('Hello World', {exact: false})
    expect(helloWorldElement).toBeInTheDocument();
}) 
```

# Finging elements

- Get
	- Thorw error if not found
- Find
	- Returns a promise
	- If element is eventually on the screen
	- React will retest until it succeeds (useful for async functions)
		- Can set timeout (default 1s)
- Query
	- Won't throw error if not found
	- Useful to check if you do not expect element to be rendered

# User Interaction

```JS
import userEvent from '@testing-library/user-event'
```

## Button Click
```JS
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
```