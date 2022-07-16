# useEffect Hook

The Effect Hook is used to call another function that does something for us so there is nothing returned when we call the useEffect() function.

The first argument passed to the useEffect() function is the **callback function** that we want React to call after **each time this component renders**. We will refer to this callback function as our effect.

```

import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
---

## Clean Up Effects

Some effects require cleanup. For example, we might want to add event listeners to some element in the DOM, beyond the JSX in our component. When we add event listeners to the DOM, it is important to remove those event listeners when we are done with them to avoid memory leaks!

Let’s consider the following effect:

```
useEffect(()=>{
  document.addEventListener('keydown', handleKeyPress);

  //clean up effects
  return () => {
    document.removeEventListener('keydown', handleKeyPress);
  };
})
```

If our effect didn’t return a cleanup function, then a new event listener would be added to the DOM’s document object every time that our component re-renders. Not only would this cause bugs, but it could cause our application performance to diminish and maybe even crash!

Because effects run after every render and not just once, React calls our cleanup function before each re-render and before unmounting to clean up each effect call.

If **our effect returns a function**, then the useEffect() Hook always treats that as a cleanup function. React will call this cleanup function before the component re-renders or unmounts. Since this cleanup function is optional, it is our responsibility to return a cleanup function from our effect when our effect code could create memory leaks.

```
import React, { useState ,useEffect} from 'react';

export default function Counter() {
  const [clickCount, setClickCount] = useState(0);
  
  useEffect(()=>{
    document.addEventListener('mousedown',increment);

    //return a clean up function here
    return ()=>{
       document.removeEventListener('mousedown',increment);
    }
  })
  // your code here
  const increment=()=>{
    setClickCount((clickCount)=> clickCount + 1)
  }

  return (
      <h1>Document Clicks: {clickCount}</h1>
  );
}

```
---

## Control When Effects Are Called

It is common, when defining function components, to run an effect only when the component mounts (renders the first time), but not when the component re-renders. The Effect Hook makes this very easy for us to do! If we want to only call our effect after the first render, we pass an empty array to useEffect() as the second argument. This second argument is called the **dependency array.**

The dependency array is used to tell the useEffect() method when to call our effect and when to skip it. Our effect is always called after the first render but only called again if something in our dependency array has changed values between renders.

Using an empty dependency array to call an effect when a component first mounts, and if a cleanup function is returned by our effect, calling that when the component unmounts.

```
useEffect(() => {
  alert("component rendered for the first time");
  return () => {
    alert("component is being removed from the DOM");
  };
}, []); 


Without passing an empty array as the second argument to the useEffect() above, those alerts would be displayed before and after every render of our component, which is clearly not when those messages are meant to be displayed. Simply, passing [] to the useEffect() function is enough to configure when the effect and cleanup functions are called!

```

---
## Fetch Data

When our effect is responsible for fetching data from a server, we pay extra close attention to when our effect is called. Unnecessary round trips back and forth between our React components and the server can be costly in terms of:

   - Processing
   - Performance
   - Data usage for mobile users
   - API service fees


An empty dependency array signals to the Effect Hook that our effect never needs to be re-run, that it doesn’t depend on anything. Specifying zero dependencies means that the result of running that effect won’t change and calling our effect once is enough.


A dependency array that is not empty signals to the Effect Hook that it can skip calling our effect after re-renders unless the value of one of the variables in our dependency array has changed. If the value of a dependency has changed, then the Effect Hook will call our effect again!


Here’s a nice example from the  [official React docs:](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects)

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if the value stored by count changes
```

---
## Rules of Hooks
There are two main rules to keep in mind when using Hooks:

1. only call Hooks at the top level
   
2. only call Hooks from React functions

we always call our Hooks at the top level; we never call hooks inside of loops, conditions, or nested functions.

```
useEffect(() => {
  if (userName !== '') {
    localStorage.setItem('savedUserName', userName);
  }
});
```
---

## Separate Hooks for Separate Effects

When multiple values are closely related and change at the same time, it can make sense to group these values in a collection like an object or array. Packaging data together can also add complexity to the code responsible for managing that data. Therefore, it is a good idea to separate concerns by managing different data with different Hooks.

```
// Handle menuItems with one useEffect hook.
const [menuItems, setMenuItems] = useState(null);
useEffect(() => {
  get('/menu').then((response) => setMenuItems(response.data));
}, []);
 
// Handle position with a separate useEffect hook.
const [position, setPosition] = useState({ x: 0, y: 0 });
useEffect(() => {
  const handleMove = (event) =>
    setPosition({ x: event.clientX, y: event.clientY });
  window.addEventListener('mousemove', handleMove);
  return () => window.removeEventListener('mousemove', handleMove);
}, []);
```
---

## Review

 - useEffect() - we can import this function from the 'react' library and call it in our function components

- effect - refers to a function that we pass as the first argument of the useEffect() function. By default, the Effect Hook calls this effect after each render

- cleanup function - the function that is optionally returned by the effect. If the effect does anything that needs to be cleaned up to prevent memory leaks, then the effect returns a cleanup function, then the Effect Hook will call this cleanup function before calling the effect again as well as when the component is being unmounted

- dependency array - this is the optional second argument that the useEffect() function can be called with in order to prevent repeatedly calling the effect when this is not needed. This array should consist of all variables that the effect depends on.

- The Effect Hook is all about scheduling when our effect’s code gets executed. We can use the dependency array to configure when our effect is called in the following ways:

Dependency Array	Effect called after first render & …
undefined	every re-render
Empty array	no re-renders
Non-empty array	when any value in the dependency array changes
Hooks gives us the flexibility to organize our code in different ways, grouping related data as well as separating concerns to keep code simple, error-free, reusable, and testable!