# Selectors

```CSS
/*element*/
button{
	property: value;
}

/*class*/
.className{
}

/*ID*/
#eleID{
}

/*nested*/
parentEle childEle{
}

/*Multiple selectors*/
button, p{
}


```


# Inheritance

For elements that are not inheriting desired property
```CSS
button{
	color: inherit;
}
```


# Transforms

```css
transform: [rotate] [skew] [scale] [translate] [perspective]
```

# Display

display:
- block
- inline
	- margin and padding only respected horizonatally inline
- inline-block
	- Sit in row but respect block element properties
- none

# Dimensions & Units

- Absolute Unit
	- px
- Relative Units
	- EM
		- Font size. Relative to parent element (2 em twice parent font size)
		- Commonly used with padding / margin (1 em relative to font size of element itself)
		- Can be used on button corners to maintain shap `font-size: 1em; padding 0 1em; border-radius: 0.5em`
	- REM
		- Nested Items can stack!
		- Root EMS. Relative to one root html element in root
		- Set in `html lang=eng`
			- `html{ font-size: 20px; }`
	- VH
	- VW
	- %
		- Relative to parent (width: 50% is half width of parent)
		- line-height: 50% (half of the front size)
		- 

# Box Shadow

```css
box-shadow: xOffset yOffset Blur Spread
```

# Background Image
```css
	background-image = url(<URL>)
	background-size: cover, contain, auto
	background-position: bottom;
```

#Flex Box
Layout items in a box of contents. Get items to go from inline with even spacing to stacked.
Able to change how items are layed out as the screen space changes.

## Two axis
- Main axis (Left to Right)
- Cross axies ( Top to bottom)

Flex direction: Decide axis (defualt row (L to R), row-reverse (R to L), column (top to bottom), column-reverse (bottom to top))

## justify-content
- flex-start (dependant on flex direction, default: left)
- flex-end
- center
- space-between (distribute space between elements but not the edge elements to container)
- space-around
- space-evenly

## flex-wrap
Wheter elements wrap on the main-axis to a new line
- wrap
- wrap-reverse (cross axis reversed)
- no-wrap (default)

## align-items
Distribute sapce along cross axis
- flex-start
- baseline (aligns to bottom of text)

## align-content
Distribute space along the cross axis with multiple rows/columns wrapping
Same properties as justify-content
Requires flex-wrap property to be set to some value

## align-self
assigned to individual elements
Change alignment on cross axis for single element

## flex-basis
Works along main axis
Overwrites width of row, height of column
Inital size that elements are added into flex box

## flex-grow
Space taken up if there is available space
Assigned to indivdual elements
```css
flex-grow: 1;
```
If you also have width assigned it can wrap
Value sets weighting
value 2 gets twice as much growth as 1

## flex-shrink
Rate elements shrink when there is not enough space in the container
Similar to flex-grow

## Shorthand
flex-grow
flex-grow flex-shrink / flex-grow flex-basis (dependant on inputs)
flex-grow flexs-shrink flex-basis
