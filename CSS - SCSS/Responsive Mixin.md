```scss
@mixin devices($breakpoint) {
	//the name of the mixin is devices

	@if $breakpoint == tablet {
		@media only screen and (min-width: 600px) {
			@content;
		}
	}

	@if $breakpoint == desktop {
		@media only screen and (min-width: 992px) {
			@content;
		}
	}
}
```

```scss
// Handling the responsiveness
.responsive {
    background: yellow;
  // The normal background color is set to yellow
 
  @include devices(tablet) {
        background: lightblue;
        // code set for tablet
    }
 
  @include devices(mobile) {
        background: aquamarine;
        h1{
            color: red;
        }
        // code set for mobile    
    }
}
```