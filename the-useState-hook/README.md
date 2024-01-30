# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

CREATOR GUIDANCE

Make a very simple demo application that initializes a value in state. Do not yet use the second, updating function in this microlesson: simply initialize several values in the state of a component. Make sure the demo app has at least two separate useState calls to demonstrate how to use multiple values and so on.

Use the values in state as part of rendering the component. 

Include an object as one of the state values to show that you can have complex data structures that live in state.

Creating a dark mode toggle application would be a reasonable use of a boolean value in state, using something like className = {lightingMode} that can be equal to .dark or .light with a pre-provided css sheet giving simple guidance on making a dark background with light text or vice versa. You could challenge students to do a psychadelic mode or 80s mode or whatever other wacky lighting modes you can think of for color schemes.

The end state of this microlesson is merely to have a value that lives in state and is used as part of the rendering, so this should be a short one. The actual toggling will come in the next microlesson about updating state, so no need to linger here too long.
