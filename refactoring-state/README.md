# ![React State Management - Refactoring State](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to refactor a React component's state to handle multiple modes using a string-based state variable.

## Flexible state management

In the previous lesson, we toggled between 'light' and 'dark' modes using a `boolean` state. However, real-world applications often require more versatile state management. Let’s refactor our component to use a string-based state that can accommodate multiple modes.

## Refactor the state variable

First, we’ll change our state from a `boolean` to a `string`. This will allow us to store different mode values like 'light', 'dark', or potentially others like 'sepia' or 'night'.

Update the following in `App.jsx`:

```jsx
const App = () => {
  const [mode, setMode] = useState("light");

  // Rest of the component
};
```

## Update the handleMode function

Next, we'll modify our `handleMode` function. Instead of setting the state to `true` or `false`, it will now set the mode state to a passed in `mode` string:

```jsx
const handleMode = (modeValue) => {
  setMode(modeValue);
};
```

The refactored `handleMode` function can handle any mode string passed to it. This versatility makes it easy to add new modes without modifying the function's logic. You can call `handleMode('sepia')`, `handleMode('night')`, or any other mode string, and the function will work seamlessly.

As new modes are introduced, you don't need to revisit this function to make updates, making it more maintainable.

### Potential pitfalls 

The function assumes that the passed string is a valid mode. If an invalid string is passed, it might lead to unexpected behaviors or a broken UI. For example, if `handleMode('unknownMode')` is called, the app might apply a non-existent CSS class.

While flexible, this approach can become unwieldy as the number of modes increases. If modes have distinct behaviors beyond just visual changes, managing all these within a single state variable can become challenging.

It may be necessary in the future to add conditional logic that checks a passed in mode against a list of "known" modes that have corresponding CSS classes. 

## Update the event handlers on buttons

Now, we'll update the buttons' `onClick` handlers to pass the respective mode string. 

Normally, when you use `onClick={handleMode}`, you’re telling React to call the `handleMode` function when the event occurs. However, if you need to pass an argument to `handleMode`, like 'dark' or 'light', you can't just write `onClick={handleMode('dark')}`. This would call the function immediately when the component renders, not when the button is clicked.

To ensure that `handleMode` is called with an argument only after the click event, we wrap it inside an *anonymous function*. The arrow function `() =>` doesn't execute right away; it only runs when the button is clicked.

```jsx
<button onClick={() => handleMode('dark')}>
  Dark Mode
</button>
<button onClick={() => handleMode('light')}>
  Light Mode
</button>
```

Inside the anonymous function, you can then call `handleMode('dark')`. This way, the `handleMode` function gets called with the correct parameter, but only in response to the click event.

You can now add additional buttons that pass in their own unique theme names. Don't forget to add the new themes to your CSS file!

## Apply the mode to the component

Let's refactor to use the new `mode` state to dynamically set the class for your component.

```jsx
<div className={mode}>
  <h1>Hello world!</h1>
</div>
```

## Final app component

Your final refactor in `App.jsx` should look something like this:


```jsx
// src/App.js
import { useState } from "react";
import "./App.css";

const App = () => {
  const [mode, setMode] = useState("light");

  const handleMode = (modeValue) => {
    setMode(modeValue);
  };

  return (
    <>
      <div className={mode}>
        <h1>Hello world!</h1>
      </div>
      <div>
        <button onClick={() => handleMode("dark")}>Dark Mode</button>
        <button onClick={() => handleMode("light")}>Light Mode</button>
      </div>
    </>
  );
};

export default App;
```

Great work! 

## 🎓 You Do : Add a new theme

Use the following CSS classes to add two new themes to your application.

```css
.neon {
  background-color: #0f0f0f; /* Dark background */
  color: #39ff14; /* Bright neon green text */
  border: 3px solid #39ff14; /* Neon green border */
  text-shadow: 0 0 5px #39ff14; /* Glowing text effect */
}
```

```css
.night {
  background-color: #1a1a2e; /* Deep blue night sky background */
  color: #e0e0e0; /* Soft white text for readability */
  border: 2px solid #0f3460; /* Dark blue border for depth */
}
```