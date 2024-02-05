# ![[tktk Module Name] - Concepts](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

CREATOR GUIDANCE

Describe the concept of state, particularly the **immutable** nature of variables that live in state.

Include description of the state change => re-render cycle, and that components will be re-rendered based on state changes local to that component.

BRIEFLY indicate a warning about legacy class-based component state and modern hooks based state, in particular emphasizing the need to avoid state-based components in google results and ensure you're using hooks for state management.

## React State

State is a the way to represent data in a React component. State is a JavaScirpt object holds and tracks the data that a component needs to render. Before thinking of state in terms of code let's take this to the real world and think through and example of state. 

Think of an oven. On this oven we have a couple of settings:

- Temperature
- Timer
- Light

The user of this oven can interact with these setting change them to bake a cake:

- Set the temperature to 350 degrees
- Set the timer to 30 minutes
- Use the light to check on the cake

The settings of the oven are our state. They are the data needed for the oven to operate. Just like the oven, a React component can be interacted with and can have settings that change. When that happens, the component needs to re-render to reflect the new state. This would be like if the oven's temperature changed, the oven would need to update the display to reflect the new temperature.

## Rendering State

Still thinking about state at a high level let's think a little more about how state is used in a React component. When a component is first rendered, the state is used to determine what the component looks like. When the state changes, the component needs to re-render to reflect the new state. This is the basic idea of how state is used in a React component.

Taking this back to our oven example when the user changes the temperature of the oven, the oven needs to update the display to reflect the new temperature. This is the same idea with a React component. When the state changes, the component needs to re-render to reflect the new state.

## Immutable State

State in React is immutable and should not be changed directly. React's state being immutable is important for a couple of reasons:

- Predictable Updates: Knows when a component needs to re-render
- Pure Components: A component preduces the same output given the same input

If the state is changed directly, React will not know that the state has changed and will not re-render the component. So our Pure Components will not be pure and predictable updates will not be predictable. Simple said **DO NOT CHANGE STATE DIRECTLY**.

Instead, there are built in hooks from React that allow us to change state. The most common hook for changing state is `useState`.

## Legacy State

React has been around for a little while and has gone through some growth and changes. One of the changes that has happened is the way state is managed. In the past, state was managed in class-based components. This is no longer the recommended way to manage state. The recommended way to manage state is with hooks.

When searching for information about state management in React, be sure to look for information about hooks and not class-based components. This is important because the way state is managed in class-based components is different than the way state is managed with hooks.
