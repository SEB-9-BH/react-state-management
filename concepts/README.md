# ![React State Management - Concepts](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to describe the importance of state management in React.

## React State

State is a the way to represent data in a React component. The state is a JavaScript object that holds and tracks the data a component needs to render. Before thinking of the state in terms of code, let's take this to the real world and consider an example of state. 

Think of an oven. On this oven, we have a couple of settings:

- Temperature
- Timer
- Light

The user of this oven can interact with these settings to change them to bake a cake:

- Set the temperature to 350 degrees
- Set the timer to 30 minutes
- Use the light to check on the cake

The oven settings are our state. They are the data needed for the oven to operate. The user interacting with the oven is like a user interacting with a React component. The user changes the oven settings, and the oven responds to the changes.

## Rendering State

Still thinking about the state at a high level, let's think more about how the state is used in a React component. When a component is first rendered, the state is used to determine what the component looks like. When the state changes, the component must re-render to reflect the new state. This is the basic idea of how state is used in a React component.

Taking this back to our oven example, when the user changes the oven's temperature, the oven needs to update the display to reflect the new temperature. This is the same idea with a React component. When the state changes, the component must re-render to reflect the new state.

## Immutable State

State in React is immutable and should not be changed directly. React's state being immutable is essential for a couple of reasons:

- Predictable Updates: Knows when a component needs to re-render
- Pure Components: A component produces the same output given the same input

If the state is changed directly, React will not know that the state has changed and will not re-render the component. So, our Pure Components will not be pure, and predictable updates will not be predictable. Simply said **DO NOT CHANGE STATE DIRECTLY**.

Instead, there are built-in hooks from React that allow us to change state. The most common hook for changing state is `useState`.

## Legacy State

React has been around for a while and has undergone some growth and changes. One of the changes that has happened is the way the state is managed. In the past, the state was managed in class-based components. This is no longer the recommended way to manage the state. The recommended way to manage the state is with hooks.

When searching for information about state management in React, look for information about hooks and not class-based components. This is important because the way the state is managed in class-based components is different than the way the state is managed with hooks.