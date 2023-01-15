Install with [[1 - Setup#React Router Installation]]]

- Moving between components within a single page application
- Move from page to page by displaying different components
- ppackage for web app "react-router-dom"

# Create classes for export

```jsx
export function Contact(){
  return(
    <div>
      <h1>Contact Page</h1>
    </div>
  )
}
```

# Import into index.js

```jsx
import {App, About, Contact} from './App';
import { BrowserRouter, Route, Routes } from "react-router-dom";

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <Routes>
      <Route path="/" element={<App />} />
	  <Route path="/contact" element={<Contact />} />
    </Routes>
  </BrowserRouter>
);
```

# Add in Link Navigation

```jsx
import { Link } from "react-router-dom"

export function Home() {
  return (
    <div>
      <nav>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>
      <h1>My Website Homepage</h1>
    </div>
  );
}

```

# Nesting Links

- Display as child of another page
	- Page will be displayed when visiting website.com/parent/child
- Add nested route but ommmit / in path

```jsx
<Route path="/about" element={<About />}>
	<Route path="history" element={<History />} />
</Route>
```

- Add outlet to parent Class
```jsx
import { Link, Outlet } from "react-router-dom";

export function About() {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>
      <h1>About Page</h1>
      <Outlet />
    </div>
  );
}

export function History() {
  return (
    <div>
      <h1>History</h1>
    </div>
  );
}
```