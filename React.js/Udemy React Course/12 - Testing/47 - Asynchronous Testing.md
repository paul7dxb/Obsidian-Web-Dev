- As seen in Udemy course project 'react-testing'
- Test component behaves correctly with response or lack of

```JSX
import { render, screen } from "@testing-library/react"
import Async from "./Async"

describe('Async component' , () => {
    test('renders posts if request succeeds', async() => {
        render(<Async />)

        // Check list items have been rendered
        // if you dont use all it will fail if more than 1
        const listItemElements = await screen.findAllByRole('listitem')
        expect(listItemElements).not.toHaveLength(0);
    })
})
```

# Mocks

- In testing you don't want to send a lot of genuine requests
- POST requests might interact with live database making unwanted changes
- Either
	- Don't sent requests
	- Send request to dummy server

- Jest has built in Mock support

Above example with  a mock function to simulate response:

```JS
import { render, screen } from "@testing-library/react"
import Async from "./Async"

describe('Async component' , () => {
    test('renders posts if request succeeds', async() => {
        // overwrite fetch function with mock to avoid real data requests
        // Jest dummy function
        window.fetch = jest.fn()
        // value function should resolve to
        window.fetch.mockResolvedValueOnce({
            json: async () => [{id: 'p1', title: 'First Post'}]
        });
        render(<Async />)

        // Check list items have been rendered
        // if you dont use all it will fail if more than 1
        const listItemElements = await screen.findAllByRole('listitem')
        expect(listItemElements).not.toHaveLength(0);
    })
})
```

