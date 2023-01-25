One Website and stylesheet that is able to resond to different device sizes and features

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
