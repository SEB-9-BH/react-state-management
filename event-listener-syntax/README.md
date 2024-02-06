# ![React State Management - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

## Event Listeners

React lets you respond to events through the use of built-in event handlers. These event handlers are passed custom functions which will be invoked in response to various user interactions. 

For this lesson, we'll be creating an event handler function that will `console.log()` which of two buttons has been clicked on the UI. Eventually, we'll be using these UI elements to toggle between a simple light and dark mode design, so we'll be using that language when constructing the buttons and event handlers.

Let's start with our buttons. In the body of `App.jsx`, add the following: 

```jsx
const handleMode = () => {
  // Null, we'll be adding code here in the next step
}

return (
  <>
    <button id='dark' onClick={handleMode}>Dark Mode</button>
    <button id='light' onClick={handleMode}>Light Mode</button>
  </>
);
```

Syntactically, this will look a bit similar to how HTML events are handled, but there are a few important differences to note: 

First, React events are always named using camelCase: `onClick`, `onSubmit`, etc.

Secondly, functions passed to event handlers must not be called! Since the JavaScript inside of JSX brackets executes immediately during render, invoking the function when you pass it to the event handler will cause it to fire off without a click event! 

Instead, we want to simply pass the function as a reference, and React will call the function when the user clicks the element: 

```jsx
// Incorrect: invoking the function
<button id='dark' onClick={handleMode()}>Dark Mode</button>
```
```jsx
// Correct: passing the function
<button id='dark' onClick={handleMode}>Dark Mode</button>
```

## Coding the event handler function

Conventionally, we attach a `handle` prefix for event handlers. Since this function will eventually be responsible for toggling between the two modes, a name like `handleMode` is fitting. 

Let's add some functionality to our event handler: 

```jsx
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
    <button id='dark' onClick={handleMode}>Dark Mode</button>
    <button id='light' onClick={handleMode}>Light Mode</button>
  </>
);
```

If the `id` of the button (the `event.target`) that is clicked was 'dark', then we log 'Dark Mode!'. If the `id` is 'light', then we log 'Light Mode!' But hold on - where did the `event` object come from? 

The `event` object is passed implicitly as an argument to the handler function! As a result, the only parameter in any handler function will always be the event object, which we are naming `event` in the params of `handleMode`. 

[tktk maybe reuse an existing graphic here reminding students about evt, evt.target, and evt.target.id]

Note that both buttons are being passed the *same* handler function in their `onClick` attribute. This works because `handleMode` is using conditional logic that is based on the `event`. As a result, we can use a single function to handle both button click events! 

```jsx
const App = () => {

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
        <button id='dark' onClick={handleMode}>Dark Mode</button>
        <button id='light' onClick={handleMode}>Light Mode</button>
      </div>
    </>
);
}
```

<!-- SECTION TWO: Remind students of the event object and the e.target property.
Make a demo app with two or more buttons with distinct functionality that share the same listener.

The critical part is the e.target property! -->





tktk Levelup, along with custom event handlers?
<!-- You might be thinking: 'well, that's all fine and good with simple handlers, but what about instances where I need to pass an argument to the event handler?' You can use an anonymous function to define the event handler inline: 

```jsx
<button id='dark' onClick={(e) => handleMode(e, 'an argument')}>Dark Mode</button>
```

In this case, the anonymous function is created immediately, but will only be called when a click event occurs.  -->