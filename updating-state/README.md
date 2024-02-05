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

Whatever value we provide to `setMode()` will become the new `mode` state.
When the component renders, the initial value of `mode` is set to `'light'`. 

If the user clicks on the `<button>` with `id='dark'`, then `setMode('dark')` is invoked, and our `mode` state is now 'dark'. 
If the user clicks on the `<button>` with `id='light'`, then `setMode('light')` will be invoked, and the `mode` state will change back to 'light'. 

<!-- This is also where you could demo the immutability of state by giving a nice warning section in the vein of "THIS WONT WORK AND HERES WHY" after a code snippet with `valueInState = newValue`.

[tktk mutability] -->
<!-- From Concepts -->
<!-- State in React is immutable and should not be changed directly. React's state being immutable is important for a couple of reasons:

Predictable Updates: Knows when a component needs to re-render
Pure Components: A component preduces the same output given the same input
If the state is changed directly, React will not know that the state has changed and will not re-render the component. So our Pure Components will not be pure and predictable updates will not be predictable. Simple said DO NOT CHANGE STATE DIRECTLY. -->




<!-- CREATOR GUIDANCE:

This one's got the good stuff of the lesson, where you respond to a user event by using the setState handler function. Make sure the event is still an onClick of a button for now.



Buildable demo: complete the dark mode light mode toggle, you could challenge students to create a third button with a third lighting mode.

Hold off on using inputs, as we haven't gotten to the controlled forms in react lesson yet and we don't want students using vanilla JS to access DOM elements. It requires a bit of creativity to keep using button-based apps instead of ones with legitimate inputs, but the avoidance of document.getElementById type business is the goal of doing so.

For a you-do challenge you could also leverage an app with a counter and buttons that increment or decrement (sometimes by 1, sometimes by 5 maybe?). 

A final potential suggestion application would be selecting between "characters" by clicking an image and having things on the page change both style and content based on which character you've chosen.

Use your imagination in coming up with all the button-based toggling apps your can think of! -->