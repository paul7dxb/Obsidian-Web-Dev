- Create a index.js file that willl be used to render the initial page
	- index is a special name

- Other pages are rendered based on the filename
	- E.g news.js can be found at /news

# File Based Routing

- pages is a reserved folder name for routing
- Folders act as path segments
	- Can access via index file
- Nested routes need to be created in a folder

![[NextJS_Routing.png]]

# Dynamic Paths

- Where url includes parameter
	- Special syntax using square brackets
	- paramater name inside the brackets


![[NextJS_Parameter_File_Name.png]]

- You can also use dynamic content in folder names e.g [newsId]
# Access Route Value

- Extract dynamic component of url

```JSX
// domain.com/news/newsId

import { useRouter } from 'next/router'

function DetailPage(){

  //Get access to values in the URL
  const router = useRouter();
  const newsId = router.query.newsId; //will get info on each render -> blank and then  will get the value

  // Send request to backend API using newsId

    return <h1>Page for {newsId}</h1>
    
  }
  
  export default DetailPage
```

# Navigating

## Creating Links

- Keep SPA but also allow rendered HTML is directly visiting (or SEO)

- Using a tags will fetch new page and break SPA idea
	- We want to preserve state and create better experience

- Use subpackage 'next/link' to import 'Link'

```JSX
import classes from './MainNavigation.module.css';
import Link from 'next/link';

function MainNavigation() {

  return (
    <header className={classes.header}>
      <div className={classes.logo}>React Meetups</div>
      <nav>
        <ul>
          <li>
            <Link href='/'>All Meetups</Link>
          </li>
          <li>
            <Link href='/new-meetup'>Add New Meetup</Link>
          </li>
        </ul>
      </nav>
    </header>
  );
}

export default MainNavigation;
```

# Programatically Navigating

## Using Push method

- Adds a page onto the stack of pages
- Equivalent to Link component

```JSX
import { useRouter } from "next/router";
import Card from "../ui/Card";
import classes from "./MeetupItem.module.css";

function MeetupItem(props) {
  const router = useRouter(); //NextJs router

  function showDetailsHandler() {
    router.push("/" + props.id); //Push method to navigate
  }

  return (
    <li className={classes.item}>
      <Card>
        <div className={classes.image}>
          <img src={props.image} alt={props.title} />
        </div>
        <div className={classes.content}>
          <h3>{props.title}</h3>
          <address>{props.address}</address>
        </div>
        <div className={classes.actions}>
          {/* Button Used to navigate onClick */}
          <button onClick={showDetailsHandler}>Show Details</button>
        </div>
      </Card>
    </li>
  );
}

export default MeetupItem;
```