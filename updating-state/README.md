# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

## Updating State

<!-- In practice, since intro to concept is under useState Hook -->

In the last lesson, we created two buttons and attached onClick event handlers to them. However, one thing was conspicuously absent in a lecture about state management: state!

So, next let's talk about how state fits into all of this. 

First, let's make use of a new `useState` hook: 

```jsx
const [mode, setMode] = useState('light')
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

[tktk optional mutability example]
To really drive home this point, let's look at another example. We won't build out an entire form for the purposes of demonstration, so just imagine that the object being pushed into `cats` is incoming form data, instead of being hard coded. 

```jsx
function ExampleComponent = () => {
  const [cats, setCats] = useState([
    { name: 'Myshka', breed: 'Ragdoll' },
    { name: 'Malta', breed: 'Turkish Angora' }
  ]);

  const addCat = () => {
    cats.push({ name: 'Kira', breed: 'Ragamuffin' })
  };

  return (
    <>
    <button onClick={addCat}>Add Cat</button>
    <ul>
      {cats.map((cat, idx) => <li key={idx}> cat.name </li>)}
    </ul>
    <>
  );
};
```

Normally, we'd expect this to work - when the user clicks the button, we add the new cat object to our `cats` array using the `push()` method. However, our list of cats won't update to reflect the changes, for two reasons! 

First, React doesn't 'know' that state has changed. We can fix that by passing our mutated array to `setCats`: 

```jsx
  const addCat = () => {
    cats.push({ name: 'Kira', breed: 'Ragamuffin' })
    setCats(cats)
  };

```

React still won't update our cats list! That's because, even if you do alert React to a change, React is going to determine if it should re-render based on a comparison between the old value (`state`), and the new value (`nextState`, as provided to our state setter function). To React, both the old value and the new value are just pointing to the same array in memory, so React will skip re-rendering. 

This is why we need to maintain immutability - instead of mutating the array, we need to make a copy of the original array, make changes to that copy, and then replace the original with it. 

[tktk end sidebar]

## Using State

With that out of the way, we can use our state to set the styling of our app! In our `App.css` file, we have some simple styling for both `light` and `dark` classes. If we create a container `<div>` for our buttons, we can pass our `mode` state as the class name: 

```jsx
const App = () => {
  const [mode, setMode] = useState('light');

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      setMode('dark');
    };
    if (event.target.id === 'light') {
      setMode('light');
    };
  };

  return (
    <div className={mode}>
      <button id='dark' onClick={handleMode}>Dark Mode</button>
      <button id='light' onClick={handleMode}>Light Mode</button>
    </div>
  );

export default App
};
```

> Remember that we camelCase attributes in JSX! 

The initial state of `mode` is 'light', so when the page initially renders our 'light' class styling will be applied. Try clicking on the 'Dark Mode' button, and see what happens! 

## Building a toggle

Let's explore another possibility for implementing a dark mode in our App.
First, we'll make some new state - this time, rather than keeping track of a specific string, our state will be a Boolean that keeps track of if the app should be in dark mode or not. As a result, we'll call it `isDarkMode`, and give it an initial value of `false`: 

```jsx
const App = () => {
  const [mode, setMode] = useState('light');
  // Add the following: 
  const [isDarkMode, setIsDarkMode] = useState(false);

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      setMode('dark');
    }
    if (event.target.id === 'light') {
      setMode('light');
    }
  }

  return (
    <div className={mode}>
      <button id='dark' onClick={handleMode}>Dark Mode</button>
      <button id='light' onClick={handleMode}>Light Mode</button>
    </div>
  );
}

export default App
```

Next, we'll need a button that the user can click to toggle our state.
You'll notice something new in the event handler `handleDarkMode`. We can pass `setState` a function - this function will automatically receive the previous state as an argument. As a result, we can update state based on this previous state, which is useful when creating a toggle: 

```jsx
const App = () => {
  const [mode, setMode] = useState('light');
  const [isDarkMode, setIsDarkMode] = useState(false);

  const handleDarkMode = () => {
    setIsDarkMode(prevState => !prevState);
  }

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      setMode('dark');
    }
    if (event.target.id === 'light') {
      setMode('light');
    }
  }

  return (
    <>
      <div className={isDarkMode && 'dark'}>  
        <button onClick={handleDarkMode}>Toggle Dark Mode</button>
      </div>

      <div className={mode}>
        <button id='dark' onClick={handleMode}>Dark Mode</button>
        <button id='light' onClick={handleMode}>Light Mode</button>
      </div>
    </>
  );
}

export default App
```

If `isDarkMode` is true, then we want the className to be 'dark'. As our 'light' mode is realistically just the default CSS styling, we only need to apply a class name in the instance that we need to apply 'dark' styling. We'll also need to add a JSX fragment (<></>) because we're now returning multiple elements. 

There you have it, two different ways to use state to implement a React-ive light and dark mode! 

