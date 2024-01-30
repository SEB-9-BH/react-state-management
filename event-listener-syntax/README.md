# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

Notes for creating this:

Demo a very simple click handler, defining a function then using the onClick={functionName} syntax. It should just do an alert or console.log for now, but state is coming next so don't manipulate state. You can TEASE state but do not include it here.
Emphasize that now you must use camelcase for onClick, onChange, etc. React has its own versions of all the builtins and you should use them.
You might talk about the virtual dom a bit, don't get too in the weeds, but the main point should be that React is in charge of the DOM and you should always try to work through react when doing DOM stuff. 

SECTION TWO: Remind students of the event object and the e.target property.
Make a demo app with two or more buttons with distinct functionality that share the same listener. The simplest thing could be a counter with an increment and decrement button, and the listener uses `e.target.value` to determine which operation to perform.
The critical part is the e.target property!
AVOID using inputs in this section, as it will only complicated things later when we introduce the controlled forms pattern. Putting an input here would invite people to start doing direct DOM access like document.getElementById() which we want to strongly discourage due to virtual DOM v real DOM power struggles.
This may very well be a refresh of stuff learned in unit 1, and that's OK!