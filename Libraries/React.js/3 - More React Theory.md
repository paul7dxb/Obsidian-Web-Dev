# How it works

![[Image_React_How_It_Works.png]]

- React to Real DOM
	- Uses Virtual Dom
	- React determines how compoenent tree looks and how it should look
	- Components re evaluated
		- Not neccessarily re rendered
		- Real DOM on changes where there are differences
			- Helps with performance as most checks are done on memory instead of rendered real DOM
			- Virtual DOM differences

![[Image_React_Component_To_DOM.png]]

