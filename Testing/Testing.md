![[Image_testing_categories.png]]

![[Image_Unit_Testing.png]]

![[Pasted image 20230711104020.png]]

![[Pasted image 20230711105012.png]]

![[Pasted image 20230711105253.png]]

# Setup Blocks

```JS
describe('Pawn', () => {

    let board;
    beforeEach(() => board = new Board());

	// Can now use in each case 
```

# Parameterised Tests

- Define test values
# Test Coverage

- How much of the code is covered by testing

![[Image_test_coverage.png]]

# Golden Master Test

- (Golden Record Test)
- Regression testing

- Make sure things haven't broken
- Throw as much data at method you know works
	- Snapshot the output data
	- Create test using same data and known correct output
	- Can make changes and expect same result

- 