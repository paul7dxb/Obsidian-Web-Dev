# [Path](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Basic_Shapes#path)

- A [`<path>`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/path) is the most general shape that can be used in SVG. 
- Using a `path` element, you can draw rectangles (with or without rounded corners), circles, ellipses, polylines, and polygons. Basically any of the other types of shapes, bezier curves, quadratic curves, and many more.
- [Paths Examples](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths)

```
<path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
```

# Commands

- M: Move to
	-  M x y
- L: Line to
	- L x y
- H: Horizontal Line
	- H x
- V: Vertical Line
	- V y
- Z: Close path

- Lowercase commands move relative to last position

- C: Cubic curve
	- C x1 y1, x2 y2, x y
	-  (x1, y1): curve start control point
	-  (x2, y2): curve end control point
	- (x, y): Where the line should end

# Examples

## Rectangle
```HTML
<!-- Move to (10,10), horizontal to x=90, vertical to y=90, vertical to x=10, line to (10,10)  -->
<path d="M 10 10 H 90 V 90 H 10 L 10 10"/>

<!-- Hollow square same dimensions  -->
<path d="M 10 10 H 90 V 90 H 10 Z" fill="transparent" stroke="black"/>

<!-- Using relative dimensions  -->
<path d="M 10 10 h 80 v 80 h -80 Z" fill="transparent" stroke="black"/>
```

## Curves

![[Image_SVG_Cubic_Curve.png]]