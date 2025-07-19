# Create Class names from variables

```scss
$bgColors: (
backgroundColor: #022c43,
background800: #18415b,
background700: #275371,
background600: #366788,
background500: #447599,
background400: #5f89ab,
background300: #789ebe,
background200: #99bbd7,
background100: #b8d7f0,
background50: #dcefff
);
	
@each $name, $hex in $bgColors {
  .#{$name} {
    background-color: $hex;
  }
}
```

