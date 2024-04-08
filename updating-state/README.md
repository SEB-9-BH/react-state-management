# ![React State Management - Updating State](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to update state using a setter function in a React component.

## Updating state

In the last lesson, we created two buttons and attached `onClick` event handlers to them. This allowed us to show a message in the console indicating we toggled between the light and dark modes. However, we didn't actually change the state of our component. Let's do that now!

Adjust the `handleMode()` function to finally make use of the setter function `setIsDarkMode`:

```jsx
  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      setIsDarkMode(true);
    } else if (event.target.id === 'light') {
      setIsDarkMode(false);
    }
  };
```

When the user clicks the **Dark Mode** button with `id='dark'`, the setter function `setIsDarkMode(true)` is called, changing the `class` on the first `<div>` to `dark`.

Conversely, clicking the **Light Mode** button with `id='light'` calls the `setIsDarkMode(false)` setter function. This will change the `class` on the first `<div>` to `light`.

When state changes, the component (and its UI) in which that state changed is discarded, along with all of its children. All information not held in state (or by other hooks) is discarded. The component is re-rendered. Data derived from state is recomputed. The UI for the component (and its children) is refreshed, reflecting the changes that have been made to state.

tktk Hunter I think an asset would really help here, something kinda like the below, but maybe with an intermediary step where the old UI is discarded? Not sure.

![tktk state changing](./assets/state-change-tktk.png)

> 🧠 Any changes you make to state will not be immediate. Instead, they take effect at the beginning of the next render of the component.
>
> The good news is that React automatically handles this. After a setter function like `setIsDarkMode()` runs, React queues up a re-render, so your UI reflects the changes that have occrred in state changes are reflected in the UI.

Recall that state in React is immutable and should never be changed directly. An example of attempting to mutate state directly might look something like this:

```jsx
// ! Don't do this!!
  const handleMode = (event) => {
    if (event.target.id === "dark") {
      isDarkMode = true;
    } else if (event.target.id === 'light') {
      isDarkMode = false;
    }
  };
```

React only knows to re-render after a setter function is called. When state is directly changed, React is left in the dark, which causes state to de-sync from the UI.

## Using state

tktk Hunter, Could you add a CHD of state changing here? We'll probably need to talk though how this looks, since whe haven't had to show state changes yet.

After updating our handler function, we should now be able to use our buttons to change the state of our application from 'light' to 'dark' mode.

```jsx
// src/App.js

import { useState } from 'react';
import './App.css';

const App = () => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  const handleMode = (event) => {
    if (event.target.id === 'dark') {
      setIsDarkMode(true);
    } else if (event.target.id === 'light') {
      setIsDarkMode(false);
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

Great work!
