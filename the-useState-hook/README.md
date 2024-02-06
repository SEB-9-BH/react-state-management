# ![[tktk Module Name] - The `useState` Hook](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to use the `useState` hook to create stateful components.

## Creating State

State is created in a React component using the `useState` hook. The `useState` hook is a function that returns an array with two elements. 

1. The current state value
2. A function that allows you to update the state value

For this section, we will focus on the following:

- Create a state value
- Assigning an initial state value
- Visually displaying the state value

At the end of this lesson, we will have a button clicked to change the state value, but for now, let's just set the state value up. We will use the `useState` hook to create a state variable called `isDarkMode` and a function to update the state called `setIsDarkMode`. First, import `useState` from React, then use it to create the state variable and the function to update the state.

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

> In a later section, we will dive into `setIsDarkMode` and how to use it to update the state value.

Let's add a log statement and look at the new state value `isDarkMode`.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    const [isDarkMode, setIsDarkMode] = useState();

    console.log('Our isDarkMode state value is:', isDarkMode);

    return (
        <h1>Hello world!</h1>
    );
}

export default App;
```

> Make sure your log statement is outside of the return statement.

## Initial State Value

Ensuring our app runs with `npm run dev` and our console is open in our browser on `http://localhost:5173/`, we can see that the state value is `undefined`. This is because we have not yet assigned an initial state value. If we think through the actions of a dark mode toggle, we want the initial state to be `false`. That way, we allow the user to toggle it on if they're going to.

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

Now that we can successfully log the value of our state to the console let's display the state value in our app. We will use the `isDarkMode` state value to conditionally render dark or light modes. We can do this in many different ways, but for now, let's use a simple ternary operator to conditionally render a class name.

In React, we will be reaching for ternary operators a lot. They are a great way to conditionally render content in our application. Here, we want to implement a dark mode toggle. If `isDarkMode` is true, we want to change the background color of our app to black and the text color to white. If `isDarkMode` is false, we want to change the background color of our app to white and the text color to black. Let's look at an example of this ternary operator in action.

```js
isDarkMode ? 'dark' : 'light'
```

> The CSS classes `light` and `dark` have been included during this module's `Setup` section.

The result of this ternary operation will either be the string value `dark` or `light`. We can use this result as a class name to render a dark or light mode conditionally. Let's add this to our app and see the result.

```jsx
// src/App.js
import { useState } from 'react';

const App = () => {

    const [isDarkMode, setIsDarkMode] = useState(false);

    console.log('Our isDarkMode state value is:', isDarkMode);

    // Add in the div with the className
    return (
        <div className={isDarkMode ? 'dark': 'light'}>  
            <h1>Hello world!</h1>
        </div>
    );
}

export default App;
```

If you change the initial state to `true` and check the browser, you will see that our `div` has taken on our dark mode styles. If you change the initial state to `false` and check the browser, you will see that our `div` has taken on our light mode styles.

## Building State

When building applications, it often takes a lot of work to consider what items we need to hold in the state. So let's try to keep some things in mind when thinking about what to hold in state:

- What data does the component need to render?
- What data does the component need to keep track of?
- What data does the component need to change?

These are all good things to remember and ask yourself when planning. Let's take a look at some examples of these questions in action.

### What data does the component need to render?

Are you greeting a user on their profile? Are you displaying a list of user-created books? Are you displaying a list of user-created todos? These are all examples of data that the component needs to render. Any data that might change if another user logs in should be considered for the state. 

Almost always, state items are items that we want to render or display to the user. This wonderful data can come in many forms. It can be a string, a number, a boolean, an object, or an array. This can be just about anything; luckily, the `useState` hook can hold just about anything. 

When can hold an object that represents a user:

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

### What data does the component need to keep track of?

Are we taking in any user input? Then, we need to keep track of that input. We can either leave the state values as empty strings:

```jsx
const [book, setBook] = useState({
    title: '',
    author: ''
});
```

Or we can set the state values as an initial value that might have already been provided:

```jsx
const [book, setBook] = useState({
    title: 'The Great Gatsby',
    author: 'F. Scott Fitzgerald'
});
```

### What data does the component need to change?

Sometimes, state values are used to toggle display items on and off. We saw above how to use a boolean value to toggle a dark mode on and off. We can also use a boolean value to toggle on and off a modal.

```jsx
const [isModalOpen, setIsModalOpen] = useState(false);
```

Anything that we want to change over time should be considered for the state. This can be a counter, a user input, a list of items, or a boolean value.
