# Use Cases:

- Need a list that will grow
- Sophisticated data structure
	- heap
	- stack
	- queue

# Operations

|Operation |	Description |	Time complexity |	Mutates structure|
| --- | --- | --- | --- |
|find(value) 	|Returns a pointer to the node containing value in the data field, or NULL if it isn't in the list. This method can be used for membership checking as well. 	|O(N) |	No
|find(index) 	|Returns a pointer to the indexth node from the head pointer, or NULL if index is longer than the length of the list. 	|O(index) 	|No
|addBeginning(value) 	|Adds a new node with a data field containing value to the beginning of the list 	|O(1) 	|Yes
|addAfter(value, n) 	|Adds a new node with a data field containing value after node n 	|O(1) 	|Yes
|remove(value) 	|Removes first instance of value from list 	|O(N) if we need to find the element.|	Yes
|removeNextElement(n) 	|Removes node after n |	O(1) 	|Yes
|removeThisElement(n) 	|Removes node n 	|O(1) on doubly linked-list |	Yes

# Examples
