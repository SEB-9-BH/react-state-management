# ![React State Management - Updating State](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to update state in a React component. 

## Updating State

In the last lesson, we created two buttons and attached onClick event handlers to them. However, one thing was conspicuously absent in a lecture about state management: state!

So, next let's talk about how state fits into all of this. 

First, let's make use of a new `useState` hook. Add the following to `App.jsx`:

```jsx
const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);
  // Add mode state: 
  const [mode, setMode] = useState('light')
  
}
```
We'll create new state named `mode`, and give it an initial value of `'light'`. 

Next, let's make some changes to our `handleMode()` function. Instead of just `console.log()`-ing a string, we want to set our `mode` state to reflect whichever button the user clicked. Luckily, the `useState` hook makes this process pretty simply - when we destructure the array that `useState()` returns, we get both the state itself as well as a state setter function. Above, we named this state setter function `setMode()`. 

Let's adjust our `handleMode()` function to make use of these state setter functions:

```jsx
const handleMode = (event) => {
  if (event.target.id === 'dark') {
    setMode('dark');
  }
  if (event.target.id === 'light') {
    setMode('light');
  }
}
```

Whatever value we provide to `setMode()` will become the next `mode` state.
When the component renders, the initial value of `mode` is set to `'light'`. 

If the user clicks on the `<button>` with `id='dark'`, then `setMode('dark')` is invoked, and our `mode` state becomes 'dark'.
If the user clicks on the `<button>` with `id='light'`, then `setMode('light')` will be invoked, and the `mode` state will change back to 'light'. 

> 🧠 In both cases, the change to our state only takes place at the start of the next render. Luckily, React will automatically re-render after all event handlers have run.

Recall that State in React is immutable, and should not be changed directly. An example of attempting to directly mutate state would look something like this: 

```jsx
// Don't do this!! 
const handleMode = (event) => {
  if (event.target.id === 'dark') {
    mode = 'dark'
  }
  if (event.target.id === 'light') {
    mode = 'light'
  }
}
```

We mentioned above that React knows to re-render after a `setState` function runs. When state is directly changed, React is left in the dark, and this causes state to de-sync from the UI. 

## Using State

With that out of the way, we can use our state to set the styling of our app! In our `App.css` file, we have some simple styling for both `light` and `dark` classes. If we create a container `<div>` for our buttons, we can pass our `mode` state as the class name: 

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);
  const [mode, setMode] = useState('light');

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      console.log('Dark Mode!')
    }
    if (event.target.id === 'light') {
      console.log('Light Mode!')
    }
  }

  return (
      <>
        <div className={isDarkMode ? 'dark': 'light'}>  
            <h1>Hello world!</h1>
        </div>
        <div className={mode}>
            <button id='dark' onClick={handleMode}>Dark Mode</button>
            <button id='light' onClick={handleMode}>Light Mode</button>
        </div>
      </>
  );
}

export default App;
```

> Remember that we camelCase attributes in JSX! 

The initial state of `mode` is 'light', so when the page initially renders our 'light' class styling will be applied. Try clicking on the 'Dark Mode' button, and see what happens! 


## Working with Arrays

One last thing! We mentioned in the useState lesson that arrays of data will be a very common form of state when working with React applications. Let's take a look at how we can maintain immutability when working with arrays.

In the below `ExampleComponent` we have `cats` state, which is initialized as an array of objects. We also have a button which, when clicked, will invoke the `addCat` event handler. To avoid building an entire form for the purposes of demonstration, we'll just imagine that the object being passed to `addCat` is incoming form data, instead of being hard-coded. 

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

After `setCats` is invoked, React is going to determine if it should re-render based on a comparison between the old value (`state`), and the new value (`nextState`, as provided to our state setter function). 

If we didn't make a new array to pass to `setCats`, and instead just pushed the object into state directly, both the old value and the new value would just be pointing to the same array in memory. As a result, React would skip re-rendering, and the list of cats wouldn't change for the user. As you can imagine, this mismatch between the state of the app and the information rendered to the user is a big problem! 

This is why we need to maintain immutability - instead of mutating the array, we need to make a copy of the original array, make changes to that copy, and then replace the original with it! 

```jsx
  const addCat = (newCat) => {
    setCats([...cats, newCat])
  };
```