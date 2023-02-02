- No code needed backend
- Used with [API React example](https://github.com/paul7dxb/react-udemy-course/tree/master/react-movie-api-app)

- If manually adding data create nest first then set data
- Use plus sign next to parent to add child data

# Dummy data to firebase

```JS
const DUMMY_MEALS = [
  {
    id: 'm1',
    name: 'Sushi',
    description: 'Finest fish and veggies',
    price: 22.99,
  },
  {
    id: 'm2',
    name: 'Schnitzel',
    description: 'A german specialty!',
    price: 16.5,
  },
  {
    id: 'm3',
    name: 'Barbecue Burger',
    description: 'American, raw, meaty',
    price: 12.99,
  },
  {
    id: 'm4',
    name: 'Green Bowl',
    description: 'Healthy...and green...',
    price: 18.99,
  },
];
```

Make a JSON file from meals:
```JSON
{
  "meals": {
	"m1": {
	  "description": "Finest fish and veggies",
	  "name": "Sushi",
	  "price": 22.99
	},
	"m2": {
	  "description": "A german specialty!",
	  "name": "Schnitzel",
	  "price": 16.5
	},
	"m3": {
	  "description": "American, raw, meaty",
	  "name": "Barbecue Burger",
	  "price": 12.99
	},
	"m4": {
	  "description": "Healthy...and green...",
	  "name": "Green Bowl",
	  "price": 18.99
	}
  }
}
```

import JSON into firebase to give structure like this:
![[Image_Firebase_DB_Structure.png]]

# Reading in Firebase JSON data

- See more details in [[16 - HTTP Requests|React HTTP requests]] 

```JS
//send request
const response = await fetch(
  "https://react-meals-5783c-default-rtdb.firebaseio.com/meals.json"
);

//get back data
const data = await response.json();
console.log(Object.keys[0])

//store data
const loadedMeals = [];
for (const key in data){
  loadedMeals.push({
	id: key,
	name: data[key].name,
	description: data[key].description,
	price: data[key].price,
  })
}
```
