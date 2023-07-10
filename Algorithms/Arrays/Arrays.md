# Info
- Positives:
	- Array lookup time O(1)
- Negatives:
	- Adding or deleting elements to the array is `O(n)`, where `n` is the number of elements in the array.
	- Slow rearrangement

|Operation 	|Description 	|Time complexity 	|Mutates structure|
| --- | --- | --- | --- |
|append(item) 	|Adds item to the end of the list 	|O(n) 	|Yes
|delete(index) 	|Removes item from list 	|O(n) 	|Yes
|\[index\] 	|Retrieves element at index 	|O(1) 	|No
