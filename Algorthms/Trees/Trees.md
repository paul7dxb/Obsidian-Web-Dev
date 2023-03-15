- Heirarchical data
	- Root at start
	- Siblings are children of the same parent
	- Leaf at end with no children
- Parent with a reference to its children

|Operation 	|Description 	|Time complexity 	|Mutates structure|
|---|---|--|---|
|insert(obj) 	|Adds obj into the BST, while maintaining a balanced tree. 	|O(log n) 	|Yes
|delete(obj) 	|Finds and deletes obj from BST, while maintaining a balanced tree. 	|O(log n) 	|Yes
|search(obj) 	|Determines if object is in tree 	O(log n) 	No
|get(n) 	|Selects the nth highest object 	|O(log n) 	|No
|rank(rand_obj) 	|Returns the number of nodes in the BST that are less than or rand_obj. rand_obj does not have to appear in the tree. 	|O(log n) 	|No
| \<iterator\>.next() 	|Gets the next element, starting at current element 	|O(log n) 	|No
|flatten() 	|Returns a list containing the nodes in sorted order 	|O(n) 	|Implementation dependent

