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
{
	background-image = url(<URL>)
	background-size: cover, contain, auto
	background-position: bottom;
```
