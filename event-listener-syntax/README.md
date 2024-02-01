# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

Notes for creating this:

Demo a very simple click handler, defining a function then using the onClick={functionName} syntax. It should just do an alert or console.log for now, but updating state is coming next so don't manipulate state.
Emphasize that now you must use camelcase for onClick, onChange, etc. React has its own versions of all the builtins and you should use them.
You might talk about the virtual dom a bit, don't get too in the weeds, but the main point should be that React is in charge of the DOM and you should always try to work through react when doing DOM stuff. 

Buildable demo: Continue with the dark mode/light mode toggle and have them share the same event listener, but use e.target to figure out which one is being called for. Right now, just alert them to which one they're choosing.

SECTION TWO: Remind students of the event object and the e.target property.
Make a demo app with two or more buttons with distinct functionality that share the same listener.

The critical part is the e.target property!

AVOID using inputs in this section, as it will only complicated things later when we introduce the controlled forms pattern. Putting an input here would invite people to start doing direct DOM access like document.getElementById() which we want to strongly discourage due to virtual DOM v real DOM power struggles.
This may very well be a refresh of stuff learned in unit 1, and that's OK!