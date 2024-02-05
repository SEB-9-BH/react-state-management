# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

CREATOR GUIDANCE

Make a very simple demo application that initializes a value in state. Do not yet use the second, updating function in this microlesson: simply initialize several values in the state of a component. Make sure the demo app has at least two separate useState calls to demonstrate how to use multiple values and so on.

Use the values in state as part of rendering the component. 

Include an object as one of the state values to show that you can have complex data structures that live in state.

Creating a dark mode toggle application would be a reasonable use of a boolean value in state, using something like className = {lightingMode} that can be equal to .dark or .light with a pre-provided css sheet giving simple guidance on making a dark background with light text or vice versa. You could challenge students to do a psychadelic mode or 80s mode or whatever other wacky lighting modes you can think of for color schemes.

The end state of this microlesson is merely to have a value that lives in state and is used as part of the rendering, so this should be a short one. The actual toggling will come in the next microlesson about updating state, so no need to linger here too long.

## Toggle Dark Mode

In this microlesson, we will create a simple application that toggles between light and dark mode. We will use the `useState` hook to manage the state of the application. Let's think through what we need to do to make this application work. We will need:

- A button to toggle the mode
- A state variable to keep track of the mode
- A way to change the mode
- A way to display the mode

Let's begin by creating a new button. This button will have the text `Toggle Dark Mode`.

```jsx
// src/App.js

const App = () => {

  return (
    <button>Toggle Dark Mode</button>
  );
}

export default App;
```

Now that we have a button, let's add some state to our application. We will use the `useState` hook to create state variable to keep track of the mode. `useState` is a hook that allows us to add state to a function component. It returns an array with two elements:

1. The current state
2. A function that allows us to update the state

We will use the `useState` hook to create a state variable called `isDarkMode` and a function to update the state called `setIsDarkMode`. First import `useState` from React then use it to create the state variable and the function to update the state.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    const [isDarkMode, setIsDarkMode] = useState();

    return (
        <button>Toggle Dark Mode</button>
    );
}

export default App;
```

> We are using array destructuring to assign names to the elements of the array returned by `useState`.

On first load we want to make sure that `isDarkMode` is set to `false`. We want the user to toggle dark mode on only if they would like. To do this we need to set the _inital state_ of `isDarkMode` to `false`. We can do this by passing `false` as an argument to `useState`.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    // Add false to `useState`
    const [isDarkMode, setIsDarkMode] = useState(false);

    return (
        <button>Toggle Dark Mode</button>
    );
}

export default App;
```

Now that we have a state variable to keep track of the dark mode, let's add a way to change the mode. Our end goal is for a user to click on the button and toggle the dark mode on and off. Let's add an `onClick` event to the button that will call a function called `handleDarkMode`. For now, log a message to the console on click to ensure the event is working.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    const [isDarkMode, setIsDarkMode] = useState(false);

    // Add function
    const handleDarkMode = () => {
        console.log('Dark mode toggled');
    }

    // Add onClick to button element
    return (
        <button onClick={handleDarkMode}>Toggle Dark Mode</button>
    );
}

export default App;
```

We know that we should **NEVER DIRECTLY UPDATE STATE** so what do we do? We use the function `useState` returns to us. Here we have called it `setIsDarkMode`. Instead of console logging that the button has been clicked let's use this function and update the state. Since this is a boolean we are working with we can use the `!` to toggle the oposite. 

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    const [isDarkMode, setIsDarkMode] = useState(false);

    const handleDarkMode = () => {
        // Add state update here
        setIsDarkMode(!isDarkMode)
    }

    return (
        <button onClick={handleDarkMode}>Toggle Dark Mode</button>
    );
}

export default App;
```