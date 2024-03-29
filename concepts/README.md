# ![React State Management - Concepts](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to describe the concept of state in React and how it determines behavior, appearance, and the rendering and re-rendering of components.

## React state

Think of state as the "present status" or "current condition" of something. The way you are feeling right now could be described as your "emotional state."

Similarly, **_state_** in React can be thought of as the "present status" of a component. It holds the answers to questions like: has a user selected something or should the UI be different for this type of user? Under the hood, state is a dynamic data object that reflects the current attributes or conditions of a component.

## State as an analogy

To understand state in a more tangible way, let's compare a component to an everyday object - an oven. Think about the features on an oven. Most ovens have a control for temperature, an oven light, and maybe even a built in timer for tracking cooking time.

| **Oven Feature**        | **Function**                        |
| ----------------------- | ----------------------------------- |
| Control for Temperature | Sets the cooking heat.              |
| Oven Light              | Used to see inside without opening. |
| Timer                   | Tracks cooking time.                |

By interacting with these controls we, the user, have the ability to alter the state inside our oven.

| **User Interaction**          | **State Change**      |
| ----------------------------- | --------------------- |
| User sets temperature         | Temperature changes   |
| User toggles the light switch | Light turns on or off |
| User sets the timer           | Timer counts down     |

In the process of baking a cake, users interact with an oven in very specific ways, such as:

- Setting the temperature to 350 degrees
- Setting the timer to 30 minutes
- Turning on the light to check progress

In each instance, the user modifies a setting, and the oven adapts to these changes. This mirrors how a user's interactions influence a React component's state.

Much like operating an oven, interacting with a web application involves specific user actions that trigger state changes in its components. For example, clicking a button might change a component's state from 'inactive' to 'active'. Each React component, like an individual appliance, has a distinct function and maintains its own state, separate from other components.

Just as kitchen appliances collaborate to facilitate cooking, React components work together, each contributing to the overall functionality of the application. 

## Rendering State

Before a component renders for the first time, React examines its state. This initial state influences the component’s appearance and behavior, including any conditional UI elements that need to be displayed. Every time a user interacts with the component, React checks if these interactions have altered the state. If the state has changed, React automatically re-renders the component to reflect these updates.

Think of it in terms of our oven analogy: When you adjust the oven’s temperature, the oven’s display updates to show the new setting. Similarly, in a React component, any change in state leads to an update in the component’s rendering, making sure that what the user sees is always current.

This ongoing cycle of checking the state, rendering the component, and updating the render with each state change is fundamental to how React components function.

## Changing state

In React, its important to know two key things before changing a components state:

### State is *immutable*

- This means you shouldn't change the state *directly*. You wouldn’t manually turn the gears inside an oven to change the temperature. Instead, you use the oven's knobs or buttons. In React, you use special functions to update the state. This helps React keep track of when to update and show changes in your components.

### Keeps things predictable

- Because state doesn't change directly, it's easier to predict how your components will behave. Directly changing the state for a component is like an oven display showing 425 degrees when the actual temperature is different. This can cause confusion and bugs in your UI.

Simply said ***never directly alter the state object*** of a component.

## Legacy State

In React's evolution, the way we manage state has changed. Originally, state was handled with class-based components. Now, we use a simpler, more efficient method called hooks. Hooks are special functions that let you 'hook into' React features, like state management, in components. As a beginner, focus on learning hooks for state management, since they're the current standard. While you might still see class-based examples online, always refer to hooks-based approaches for managing state in your projects.
