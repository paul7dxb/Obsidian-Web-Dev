One Website and stylesheet that is able to resond to different device sizes and features

# Sizes

```CSS
 /* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...} 
```

# Media Queries
Usually screen width / device type

```css
@media param{
	selector{
		/*Styles...*/
	}
}
```

Have width 100% on small device and reduce to auto at larger size of 768px:
```css
.button{
	width: 100%;
}

@media (min-width: 768px){
	.button{
		width: auto;
	}
}
```

```CSS
@media only screen and (max-width: 768px) {

}
```
