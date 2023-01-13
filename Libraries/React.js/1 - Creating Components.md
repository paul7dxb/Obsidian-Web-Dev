# Create Element

```html
<body>
	<div id="root"></div>
</body>
```

```js
  let heading = React.createElement("h1", null, "Getting Started with React")

  ReactDOM.render(
	heading,
	document.getElementById("root")
  );
```

# Child Items

Example:
```js
let ul = React.createElement(
"ul",
{ style: { color: "blue" } },
React.createElement("li", null, "Monday"),
React.createElement("li", null, "Tuesday"),
);

ReactDOM.render(ul, document.getElementById("root"));
```

## Refactor using JSX (Javascript as XML) and Babel

Babel allows you to write XML which will then be pre processed to be used by a browser

```js
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

<script type="text/babel">
  ReactDOM.render(
	<ul>
	  <li>Monday</li>
	  <li>Tuesday</li>
	  <li>Wednesday</li>
	</ul>,

	document.getElementById("root")
  );
</script>

```

## JSX Variables

Referenced using curly brackets { }

```js
let pasta = "penne";
let pizza = "peperoni";
let iceCream = "vanilla";

ReactDOM.render(
<ul>
  <li>{pasta}</li>
  <li>{pizza}</li>
  <li>{iceCream.toUpperCase()}</li>
</ul>,

document.getElementById("root")
);

```

# Create Components

Building Block for a part of the appilcation.
Use Capital Letters for components

```js
      function Header() {
        return( 
        <header>
          <h1>Component Function Render Header</h1>
        </header>
        )
      }

      ReactDOM.render(<Header />, document.getElementById("root"));
```

# Render Multiple Components

Error: adjacent JSX elements must be wrapped in an enclosing tag
React renders single components. Make a single component that returns desired components

```js
  function Header() {
	return (
	  <header>
		<h1>Component Function Render Header</h1>
	  </header>
	);
  }

  function Main() {
	return (
	  <section>
		<p>The Paragraph in the Main component</p>
	  </section>
	);
  }

  function App() {
	return (
	  <div>
		<Header />
		<Main />
	  </div>
	);
  }

  ReactDOM.render(<App />, document.getElementById("root"));

```

# Using Props

Props is an object, gets nothing added by default

```js
  function Header(props) {
	return (
	  <header>
		<h1>Component Function Render {props.propVar}</h1>
	  </header>
	);
  }

  function Main(props) {
	return (
	  <section>
		<p>We serve the most {props.adjective} {" "} food </p>
	  </section>
	);
  }

  function Footer(props){
	return(
	  <footer>
		<p>Copyright {props.year}</p>
		</footer>
	)
  }

  function App() {
	return (
	  <div>
		<Header propVar="Prop Value"/>
		<Main adjective="amazing"/>
		<Footer year={new Date().getFullYear()}/>
	  </div>
	);
  }
```

# Using Lists

```js
function Main(props) {
return (
  <section>
	<p>We serve the most {props.adjective} food </p>
	<ul>
	  {props.dishes.map((dish) => (
		<li>{dish}</li>
	  ))}
	</ul>
  </section>
);
}
const dishes = ["Cheese sticks", "Lasagne", "Pizza"];

function App() {
return (
  <div>
	<Header propVar="Prop Value" />
	<Main adjective="amazing" dishes={dishes}/>
	<Footer year={new Date().getFullYear()} />
  </div>
);
}
```

## Child Unique Keys

Used to keep everything in Sync
Use object mapping to generate and maintain keys

```js
function Main(props) {
return (
  <section>
	<p>We serve the most {props.adjective} food </p>
	<ul>
	  {props.dishes.map((dish) => (
		<li key={dish.id}>{dish.title}</li>
	  ))}
	</ul>
  </section>
);
}
const dishes = ["Cheese sticks", "Lasagne", "Pizza"];
const dishObjects = dishes.map((dish, i) => ({
	id: i,
	title: dish
}));

function App() {
return (
  <div>
	<Main adjective="amazing" dishes={dishObjects}/>
  </div>
);
}
```

# Preventing Large DOM Trees

Having to wrap React rendering can lead to large DOM trees (lots of nested divs) before reaching the content.
Instead you can use
```js
function App() {
return (
  <React.Fragment>
	<Header propVar="Prop Value" />
	<Main adjective="amazing" dishes={dishObjects} />
	<Footer year={new Date().getFullYear()} />
  </React.Fragment>
);
}
```
