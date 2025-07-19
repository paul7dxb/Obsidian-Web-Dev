# Mixin for Mobile first

- Mixin definition:
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

- Usage:
```scss
@mixin font-subtitle() {
	font-weight: $lighterWeight;
	font-size: $mobile-font-size-subtitle;

  @include devices(tablet) {
		font-size: $tablet-font-size-subtitle;
	}
  @include devices(desktop) {
		font-size: $desktop-font-size-subtitle;
	}
}
```

```scss
.Class-name {
	font-weight: $lighterWeight;
	font-size: $mobile-font-size-subtitle;

  @include devices(tablet) {
		font-size: $tablet-font-size-subtitle;
	}
  @include devices(desktop) {
		font-size: $desktop-font-size-subtitle;
	}
}
```