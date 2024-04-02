# ![React State Management - Updating Complex State](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to update arrays in the state while maintaining immutability, using the `useState` hook

## Working with arrays in state

In our previous lesson, we focused on updating a simple boolean value in the state with React's `useState`. While toggling a boolean is straightforward and common, many real-world scenarios in React involve more complex state structures, like objects and arrays. As applications grow in complexity, you’ll often find yourself managing these more robust data types. Therefore, it's important to understand how correctly update objects and arrays in state.

Let's look at a more detailed example to illustrate this:

```jsx
import { useState } from 'react';

function ExampleComponent = () => {
  const [cats, setCats] = useState([
    { name: 'Myshka', breed: 'Ragdoll' },
    { name: 'Malta', breed: 'Turkish Angora' }
  ]);

  const addCat = (newCat) => {
    // spread current cats array and newCat object into a new array
    const newCatsArray = [...cats, newCat]
    // call state setter function with this new array
    setCats(newCatsArray)
  };

  return (
    <>
      <button onClick={() => addCat({ name: 'Kira', breed: 'Ragamuffin' })}>
        Add Cat
      </button>
      <ul>
        {cats.map((cat, idx) => <li key={idx}> {cat.name} </li>)}
      </ul>
    <>
  );
};
```

1. In this `ExampleComponent`, we're working with a state variable named `cats`, which is initialized as an array containing objects. Each object represents a cat, with properties like its name and breed. This setup is a common pattern in React applications, where you manage a list of items as an array in your state.

2. To simplify our example and focus on the state management aspect, we're directly passing a new cat object to the `addCat` function when the button is clicked. In a real-world application, this data might typically come from a form input where users can add details of a new cat. However, for our learning purposes, we use hardcoded data to demonstrate how the state updates with new items.


Here's how it works: Upon clicking the button, addCat is called with a predefined cat object. Inside addCat, we use the spread operator `...` to create a new array that contains all existing cats plus the new one. This method ensures we're *not modifying the original state directly* but creating a new updated version of it, which is a key practice in React for ensuring smooth and predictable state updates.

```js
  const addCat = (newCat) => {
    // spread current cats array and newCat object into a new array
    const newCatsArray = [...cats, newCat]
    // call state setter function with this new array
    setCats(newCatsArray)
  };
```

After `setCats` is invoked, React is going to determine if it should re-render based on a comparison between the old value `state`, and the new value `nextState`, as provided to our state setter function. 

If we didn't make a new array to pass to `setCats`, and instead just pushed the object into state directly, both the old value and the new value would just be pointing to the same array in memory. As a result, React would skip re-rendering, and the list of cats wouldn't change for the user. As you can imagine, this mismatch between the state of the app and the information rendered to the user is a big problem! 

This is why we need to maintain immutability - instead of mutating the array, we need to make a copy of the original array, make changes to that copy, and then replace the original with it! 

```jsx
  const addCat = (newCat) => {
    setCats([...cats, newCat])
  };
```