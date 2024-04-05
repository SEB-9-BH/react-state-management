# ![React State Management - Updating State](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to update state using a setter function in a React component.

## Updating State

In the last lesson, we created two buttons and attached `onClick` event handlers to them. This allowed us to toggle between 'light' and 'dark' mode being logged in the browser console, but we didn't actually change the state of our component. Let's do that now!

Let's adjust our `handleMode()` function to finally make use of the setter function `setIsDarkMode`:

```jsx
const handleMode = (event) => {
  if (event.target.id === "dark") {
    setIsDarkMode(true);
  }
  if (event.target.id === "light") {
    setIsDarkMode(false);
  }
};
```

When the user clicks the 'Dark Mode' button with `id='dark'`, the function `setIsDarkMode(true)` is called, applying the 'dark' CSS class. Conversely, clicking the 'Light Mode' button `id='light'` calls `setIsDarkMode(false)`, applying the 'light' CSS class.

> 🧠 Note: Any changes you make to state won't happen immediately. Instead, these changes take effect at the beginning of the next render of the component. The good news is that React automatically handles this. After an event handler runs, like when you click a button, React queues up a re-render, so your state changes are reflected in the UI.
>
> Recall that State in React is immutable, and should never be changed directly. An example of attempting to directly mutate state might look something like this:
>
> ```jsx
> // Don't do this!!
> const handleMode = (event) => {
>   if (event.target.id === "dark") {
>     isDarkMode = true;
>   }
>   if (event.target.id === "light") {
>     isDarkMode = false;
>   }
> };
> ```
>
> React only knows to re-render after a `setState` function is called. When state is directly changed, React is left in the dark, and this causes state to de-sync from the UI.

## Using State

After updating our handler function, we should now be able to use our buttons to change the state of our application from 'light' to 'dark' mode.

```jsx
// src/App.js

import { useState } from "react";
import "./App.css";

const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  const handleMode = (event) => {
    if (event.target.id === "dark") {
      setIsDarkMode(true);
    }
    if (event.target.id === "light") {
      setIsDarkMode(false);
    }
  };

  return (
    <>
      <div className={isDarkMode ? "dark" : "light"}>
        <h1>Hello world!</h1>
      </div>
      <div>
        <button id="dark" onClick={handleMode}>
          Dark Mode
        </button>
        <button id="light" onClick={handleMode}>
          Light Mode
        </button>
      </div>
    </>
  );
};

export default App;
```

Great work!
