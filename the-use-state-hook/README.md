# ![React State Management - The `useState` Hook](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to use the `useState` hook to create stateful components.

## Creating State

State is created in a React component using the `useState` hook. The `useState` hook is a function that returns an array with two elements: 

1. A state variable to hold your state data
2. A state setter function that allows you to update that state value and trigger the rerender of a component

For this section, we will focus on the following:

- Creating a state variable
- Assigning an initial state value
- Visually displaying that state value

Let's get to work creating our first state variable. 

First, import the `useState` hook from React. Then, we'll use a [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to unpack the two values returned from our state hook: a state variable and a setter function.

We will name our state variable `isDarkMode` and our function `setIsDarkMode`. 

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {
    const [isDarkMode, setIsDarkMode] = useState();

    return (
        <h1>Hello world!</h1>
    );
}

export default App;
```

> Destructuring Syntax: This syntax might feel unfamiliar at first, but let's take a closer look at what is happening here. Imagine `useState` as a box, when we open the box we are given two items: a variable to store data and a function to update that variable. What we name these items is up to us, but should reflect the data being stored and updated. In this case `isDarkMode` is our state variable that holds the current state (like whether dark mode is on or off), and `setIsDarkMode` is a function that let's us change or *set* this state.

> In a later section, we will dive into `setIsDarkMode` and how to use it to update the state value.


Let's add a `console.log` to take a look at our new state value `isDarkMode`:

```jsx
// src/App.js

import { useState } from 'react';

const App = () => {
    const [isDarkMode, setIsDarkMode] = useState();

    // Add a console.log
    console.log('Our isDarkMode state value is:', isDarkMode);

    return (
        <h1>Hello world!</h1>
    );
}

export default App;
```

> Make sure your console.log is outside of the return statement.

## Initial State Value

In your terminal, run:

```bash
npm run dev
```

Then navigate to:

```bash
http://localhost:5173/
```

We should see that the state value is `undefined`. This is because we have not assigned an initial state value! 

For our dark mode toggle, it makes sense to begin with the state set to `false`. This means that the app will start in 'light' mode by default.

To give our state an initial value, we just need to provide that value as an argument when calling the `useState` hook. 

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    // Update the initial state value to `false`
    const [isDarkMode, setIsDarkMode] = useState(false);

    console.log('Our isDarkMode state value is:', isDarkMode);

    return (
        <h1>Hello world!</h1>
    );
}

export default App;
```

If we recheck our console, we can see that the state value is now `false`. This is the initial state value assigned to `isDarkMode`. If you change the initial state value to `true` and recheck the console, you will see that the state value is now `true`.

## Displaying State Value

![Displaying state](./assets/state-example.png)

Now that we can successfully log the value of our state, let's use this value to alter the UI of our component. We will use the `isDarkMode` state value to conditionally render dark or light modes. We can do this in many different ways, but for simplicity, let's use a ternary operator to conditionally apply a CSS class to our component.

First we'll create a couple of simple CSS classes to define our two modes.

Replace the contents of `App.css` with the following two classes:

```css
/* src/App.css */

.light {
    background-color: #ffffff; /* white background */
    color: #333333; /* darker text for contrast */
    border-color: #dddddd; /* light grey borders */
}

.dark {
    background-color: #2c3e50; /* dark background */
    color: #ecf0f1; /* light text for contrast */
    border-color: #34495e; /* slightly darker border for depth */
}
```

> In React, we will be reaching for ternary operators a lot. They are a great way to conditionally render content in our application. If `isDarkMode` is true, we want to change the background color of our app to dark and the text color to light. If `isDarkMode` is false, we want to change the background color of our app to light and the text color to dark. 

Let's look at an example of this ternary operator in action:

```js
isDarkMode ? 'dark' : 'light'
```

The result of this operation will either be the string value `dark` or `light`. We can use this result as a class name to render a dark or light mode conditionally. Let's add this to our app and see the result.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {
    const [isDarkMode, setIsDarkMode] = useState(false);

    console.log('Our isDarkMode state value is:', isDarkMode);

    // use className to apply styles in react
    return (
        <div className={isDarkMode ? 'dark': 'light'}>  
            <h1>Hello world!</h1>
        </div>
    );
}

export default App;
```

If you change the initial state to `true` and check the browser, you will see that our component has taken on some dark mode styling. If you change the initial state to `false`, you will see that our component has taken on our light mode styling.

## Building State

When building React applications, one big consideration to make is what items we need to hold in state. So let's try to keep some things in mind when thinking about what to hold in state:

- What data does the component need to render?
- What data does the component need to keep track of?
- What data does the component need to change?

These are all good things to remember and ask yourself when planning - let's take a look at some examples of these questions in action.

### What data does the component need to render?

Are you greeting a user on their profile? Are you displaying a list of user-created books? Are you displaying a list of user-created todos? These are all examples of data that the component needs to render. Any data that might change if another user logs in should be considered for the state. 

State items are almost always items that we want to render or display to the user. This wonderful data can come in many forms; it can be a string, a number, a boolean, an object, or an array - just about anything. Luckily, the `useState` hook can hold just about anything as well! 

We can hold an object that represents a user:

```jsx
const [user, setUser] = useState({
    name: 'John Doe',
    age: 25,
    email: 'johnDoe@mail.com'
});
```

We can hold an array of objects. This can be useful if we are working with an API or a CRUD application:

```jsx
const [books, setBooks] = useState([
    {
        title: 'The Great Gatsby',
        author: 'F. Scott Fitzgerald'
    },
    {
        title: 'To Kill a Mockingbird',
        author: 'Harper Lee'
    }
]);
```

Or it can be as simple as saving a string or a number:

```jsx
const [count, setCount] = useState(0);
const [name, setName] = useState('John Doe');
```

### What data does the component need to change?

Sometimes, state values are used to toggle display items on and off. We saw above how to use a boolean value to toggle a dark mode on and off. We can also use a boolean value to toggle on and off a modal. 

```jsx
const [isModalOpen, setIsModalOpen] = useState(false);
```

These are good questions to ask yourself when planning out your state. State is a powerful tool, and it's important to use it wisely. 

## 🎓 You do: Create a new State Item

Using what you learned above, create new state with an initial value that is an object with the following properties:

- `firstName` - The value should be a string of your name.
- `lastName` - The value should be a string of your last name.
- `hasPets` - The value should be a boolean of whether or not you have pets.
- `age` - The value should be a number of your age.

Then, log the state value to the console and display the state value in the app. If all goes well, challenge yourself by displaying the state value in a sentence. For example, `"Hello, my name is John Doe, I am 25 years old, and I have pets."`