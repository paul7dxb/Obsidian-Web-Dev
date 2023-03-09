- Example used in [react-replace-redux-hooks](https://github.com/paul7dxb/react-udemy-course/tree/master/react-replace-redux/react-replace-redux-hooks) project
- A possible alternative to using Redux

Abstract Store to build individual stores:
```JS
import { useEffect, useState } from "react";

// Values exist outside of hook so will be the same to all components that import the file
let globalState = {};
let listeners = [];
let actions = {};

// Should Listen used to optimise listeners (if a component is only being used to dispatch functions)
export const useStore = (shouldListen = true) => {
  const setState = useState(globalState)[1];

  // Get action based off of a passed in identifier found in actions
  const dispatch = (actionIdentifier, payload) => {
    // call action method using brackets. Get new state based on globalState
    const newState = actions[actionIdentifier](globalState, payload);
    // Merge globalState with newState
    globalState = { ...globalState, ...newState };

    // Update react state with new global sate so rerender components using the hook
    for (const listener of listeners) {
      listener(globalState);
    }
  };

  // Add component to listeners when it mounts
  useEffect(() => {
    if (shouldListen) {
      listeners.push(setState);
    }

    // Remove when unmounts
    return () => {
      if (shouldListen) {
        listeners = listeners.filter((li) => li !== setState);
      }
    };
  }, [setState, shouldListen]);

  return [globalState, dispatch];
};

export const initStore = (userActions, initialState) => {
  if (initialState) {
    // global state is shared so need to keep current state
    globalState = { ...globalState, ...initialState };

    actions = { ...actions, ...userActions };
  }
};

```


Make a specific store
```JS
import { initStore } from "./store";

const configureStore = () => {
  const actions = {
    TOGGLE_FAV: (curState, productId) => {
      const prodIndex = curState.products.findIndex((p) => p.id === productId);
      const newFavStatus = !curState.products[prodIndex].isFavorite;
      const updatedProducts = [...curState.products];
      updatedProducts[prodIndex] = {
        ...curState.products[prodIndex],
        isFavorite: newFavStatus,
      };
      return { products: updatedProducts };
    },
  };
  initStore(actions, {
    products: [
      {
        id: "p1",
        title: "Red Scarf",
        description: "A pretty red scarf.",
        isFavorite: false,
      },
      {
        id: "p2",
        title: "Blue T-Shirt",
        description: "A pretty blue t-shirt.",
        isFavorite: false,
      },
      {
        id: "p3",
        title: "Green Trousers",
        description: "A pair of lightly green trousers.",
        isFavorite: false,
      },
      {
        id: "p4",
        title: "Orange Hat",
        description: "Street style! An orange hat.",
        isFavorite: false,
      },
    ],
  });
};

export default configureStore;
```


Initialise Store in index.js:
```JS
import configureStore from "./hooks-store/products-store";
// Call configure store for each store "part" of the application
configureStore();
```

Use Store in components:

Listing Products:
```JSX
import React, { useContext } from 'react';
import ProductItem from '../components/Products/ProductItem';
import { useStore } from '../hooks-store/store';
import './Products.css';

const Products = props => {

  //Gets the global state
  const state = useStore()[0];

  return (
    <ul className="products-list">
      {state.products.map(prod => (
        <ProductItem
          key={prod.id}
          id={prod.id}
          title={prod.title}
          description={prod.description}
          isFav={prod.isFavorite}
        />
      ))}
    </ul>
  );
};

export default Products;

```


Using actions to change the store data:

ProductItem.js:

```JSX
import React, { useContext } from "react";

import Card from "../UI/Card";
import "./ProductItem.css";
import { useStore } from "../../hooks-store/store";

const ProductItem = (props) => {

  // Get dispatch function for store
  const dispatch = useStore(false)[1];


  const toggleFavHandler = () => {
    dispatch('TOGGLE_FAV', props.id)
  };

  return (
    <Card style={{ marginBottom: "1rem" }}>
      <div className="product-item">
        <h2 className={props.isFav ? "is-fav" : ""}>{props.title}</h2>
        <p>{props.description}</p>
        <button
          className={!props.isFav ? "button-outline" : ""}
          onClick={toggleFavHandler}
        >
          {props.isFav ? "Un-Favorite" : "Favorite"}
        </button>
      </div>
    </Card>
  );
};

export default ProductItem;
```

