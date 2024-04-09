# ![React State Management - Event Listener Syntax](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to respond to events with event handler functions.

## Event listeners

React lets you respond to events using built-in event handlers. These event handlers are passed custom functions that will be invoked in response to specific user actions.

In this lesson, we'll create a function that responds to button clicks. This function will display a message in the console, telling us which button was clicked. We'll use two buttons for this: one to represent 'Light Mode' and the other for 'Dark Mode'.

Later, we'll refactor these buttons to actually switch the app's design between light and dark modes. For now, let's focus on setting up the buttons and ensuring our function can identify which one is clicked.

Let's start by creating two buttons and a placeholder for our handler function. Add the new code for this in `App.jsx`:

```jsx
// src/App.jsx

import { useState } from 'react';
import './App.css';

const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  // placeholder function for handling mode changes
  // we'll implement the functionality in the next step
  const handleMode = () => {
    // TODO: implement the logic to toggle dark and light mode
  };

  // add a new div with buttons inside
  // wrap both divs in a fragment
  return (
    <>
      <div className={isDarkMode ? 'dark' : 'light'}>
        <h1>Hello world!</h1>
      </div>
      <div>
        <button id="dark" onClick={handleMode}>Dark Mode</button>
        <button id="light" onClick={handleMode}>Light Mode</button>
      </div>
    </>
  );
};

export default App;
```

In React, handling events in the UI looks similar to how it's done in HTML, but with a few key differences to keep in mind:

1. First, React events are always named using camelCase: `onClick`, `onSubmit`, etc.

2. Secondly, when you assign a function to an event handler in React, remember not to call the function directly. Since the JavaScript inside JSX brackets executes immediately during render, invoking the function when you pass it to the event handler will cause it to fire off without a click event!

Instead, we only want to pass the function as a reference, and React will call the function when the user clicks the element:

- ***Incorrect*** (function is invoked immediately)

  ```jsx
  <button id='dark' onClick={handleMode()}>Dark Mode</button>
  ```

- ***Correct*** (function is passed as a reference and will be called on click)

  ```jsx
  <button id='dark' onClick={handleMode}>Dark Mode</button>
  ```

## Creating an event handler function

Conventionally, we attach a `handle` prefix to the name of event handler functions. Since this function will eventually be responsible for toggling between the two modes, a name like `handleMode` is fitting.

Let's add some logic to our event handler function:

```jsx
// src/App.jsx

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      console.log('Dark Mode!');
    } else if (event.target.id === 'light') {
      console.log('Light Mode!');
    }
  };
```

When one of our buttons is clicked, we want to log a message based on which button it was – 'Dark Mode!' for the dark button and 'Light Mode!' for the light button. But how do we know which button was clicked? This is where the `event` object comes in.

Every time a button is clicked, React automatically sends an `event` object to the handler function. This object contains information about the event, including which element was clicked. In our `handleMode()` function, we receive this event object as a parameter. By checking the `id` property of `event.target` (the clicked element), we can determine which button was clicked.

Here's the interesting part: both buttons use the same `handleMode()` function for their `onClick` event. This works because, inside `handleMode()`, we use the event object to check which button was clicked and respond accordingly. So, with one function, we can handle clicks for both buttons!

```jsx
// src/App.jsx

import { useState } from 'react';
import './App.css';

const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      console.log('Dark Mode!');
    } else if (event.target.id === 'light') {
      console.log('Light Mode!');
    }
  };

  return (
    <>
      <div className={isDarkMode ? 'dark' : 'light'}>
        <h1>Hello world!</h1>
      </div>
      <div>
        <button id="dark" onClick={handleMode}>Dark Mode</button>
        <button id="light" onClick={handleMode}>Light Mode</button>
      </div>
    </>
  );
};

export default App;
```

Test your buttons to make sure the correct mode is logged to the console. Nice job!
