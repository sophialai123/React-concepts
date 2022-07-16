## Function Components and Props

Like any component, function components can receive information via props.

To access these props, give your function component a parameter named props. Within the function body, you can access the props using this pattern: props.propertyName. You don’t need to use the this keyword.

```
export function YesNoQuestion (props) {
  return (
    <div>
      <p>{props.prompt}</p>
      <input value="Yes" />
      <input value="No" />
    </div>
  );
}
 
ReactDOM.render(
  <YesNoQuestion prompt="Have you eaten an apple today?" />,
  document.getElementById('app');
);

```

- Function components are React components defined as JavaScript functions

- Function components must return JSX

- Function components may accept a props parameter. Expect it to be a JavaScript object

---

## Hooks

React offers a number of built-in Hooks. A few of these include useState(), useEffect(), useContext(), useReducer(), and useRef(). See the [full list in the docs](https://reactjs.org/docs/hooks-reference.html). In this lesson, we’ll learn different ways to manage state in a function component.


---

## Update Function Component State

useState() is a JavaScript function defined in the React library. When we call this function, it returns an array with two values:

  - current state - the current value of this state
  
  - state setter - a function that we can use to update the value of this state

```
import React, { useState } from "react";
 
function Toggle() {
  const [toggle, setToggle] = useState();
 
  return (
    <div>
      <p>The toggle is {toggle}</p>
      <button onClick={() => setToggle("On")}>On</button>
      <button onClick={() => setToggle("Off")}>Off</button>
    </div>
  );
}
```

Calling the state setter signals to React that the component needs to re-render, so the whole function defining the component is called again. The magic of useState() is that it allows React to keep track of the current value of state from one render to the next!

---
## Initialize State

To initialize our state with any value we want, we simply pass the initial value as an argument to the useState() function call.

```
const [isLoading, setIsLoading] = useState(true);
```
There are three ways in which this code affects our component:

 1. During the first render, the initial state argument is used.
   
 2. When the state setter is called, React ignores the initial state argument and uses the new value.
   
 3. When the component re-renders for any other reason, React continues to use the same value from the previous render.

If we don’t pass an initial value when calling useState(), then the current value of the state during the first render will be undefined. Often, this is perfectly fine for the machines, but it can be unclear to the humans reading our code. So, we prefer to explicitly initialize our state. If we don’t have the value needed during the first render, we can explicitly pass null instead of just passively leaving the value as undefined.

---
## Use State Setter Outside of JSX

```
import React, {useState} from 'react';

// regex to match numbers between 1 and 10 digits long
const validPhoneNumber = /^\d{1,10}$/;

export default function PhoneNumber() {
  // declare current state and state setter 
  const [phone, setPhone]  = useState('')

  const handleChange = ({ target })=> {
    const newPhone = target.value;
    const isValid = validPhoneNumber.test(newPhone);
    if (isValid) {
        // update state 
        setPhone(newPhone)
    }
    // just ignore the event, when new value is invalid
  };

  return (
    <div className='phone'>
      <label for='phone-input'>Phone: </label>
      <input value={phone} id='phone-input' onChange={handleChange} />
    </div>
  );
}

```

---
## Set From Previous State

Often, the next value of our state is calculated using the current state. In this case, it is best practice to update state with a callback function. If we do not, we risk capturing outdated, or “stale”, state values.

```
import React, { useState } from 'react';
 
export default function Counter() {
  const [count, setCount] = useState(0);
 
  const increment = () => setCount(prevCount => prevCount + 1);
 
  return (
    <div>
      <p>Wow, you've clicked that button: {count} times</p>
      <button onClick={increment}>Click here!</button>
    </div>
  );
}
```

When the button is pressed, the increment() event handler is called. Inside of this function, we use our setCount() state setter in a new way! Because the next value of count depends on the previous value of count, we pass a callback function as the argument for setCount() instead of a value


When our state setter calls the callback function, this state setter callback function takes our previous count as an argument. The value returned by this state setter callback function is used as the next value of count (in this case prevCount + 1). Note: We can just call setCount(count +1) and it would work the same in this example… but for reasons that are out of scope for this lesson, it is safer to use the callback method. If you’d like to learn more about why the callback method is safer, this section of the [docs](https://reactjs.org/docs/react-component.html#setstate) is a great place to start.


---
## Arrays in State

```
import React, { useState } from "react";
 
const options = ["Bell Pepper", "Sausage", "Pepperoni", "Pineapple"];
 
export default function PersonalPizza() {
  const [selected, setSelected] = useState([]);
 
  const toggleTopping = ({target}) => {
    const clickedTopping = target.value;
    setSelected((prev) => {
     // check if clicked topping is already selected
      if (prev.includes(clickedTopping)) {
        // filter the clicked topping out of state
        return prev.filter(t => t !== clickedTopping);
      } else {
        // add the clicked topping to our state
        return [clickedTopping, ...prev];
      }
    });
  };
 
  return (
    <div>
      {options.map(option => (
        <button value={option} onClick={toggleTopping} key={option}>
          {selected.includes(option) ? "Remove " : "Add "}
          {option}
        </button>
      ))}
      <p>Order a {selected.join(", ")} pizza</p>
    </div>
  );
}
```

JavaScript arrays are the best data model for managing and rendering JSX lists. In this example, we are using two arrays:

 1. options is an array that contains the names of all of the pizza toppings available
 2. selected is an array representing the selected toppings for our personal pizza

The options array contains static data, meaning that it does not change. We like to define static data models outside of our function components since they don’t need to be recreated each time our component re-renders. In our JSX, we use the map method to render a button for each of the toppings in our options array.

The selected array contains dynamic data, meaning that it changes, usually based on a user’s actions. We initialize selected as an empty array. When a button is clicked, the toggleTopping event handler is called. Notice how this event handler uses information from the event object to determine which topping was clicked.

When updating an array in state, we do not just add new data to the previous array. We replace the previous array with a brand new array. This means that any information that we want to save from the previous array needs to be explicitly copied over to our new array. That’s what this spread syntax does for us: ...prev.

---

## Objects in State

```
export default function Login() {
  const [formState, setFormState] = useState({});
 
  const handleChange = ({ target }) => {
    const { name, value } = target;
    setFormState((prev) => ({
      ...prev,
      [name]: value //[name]is a string
    }));
  };
 
  return (
    <form>
      <input
        value={formState.firstName}
        onChange={handleChange}
        name="firstName"
        type="text"
      />
      <input
        value={formState.password}
        onChange={handleChange}
        type="password"
        name="password"
      />
    </form>
  );
}
```

A few things to notice:

1. We use a state setter callback function to update state based on the previous value

2. The spread syntax is the same for objects as for arrays: { ...oldObject, newKey: newValue }

3. We reuse our event handler across multiple inputs by using the input tag’s name attribute to identify which input the change event came from


 when updating the state with setFormState() inside a function component, **we do not modify the same object. We must copy over the values from the previous object when setting the next value of state.** Thankfully, the spread syntax makes this super easy to do!


 Anytime one of the input values is updated, the handleChange() function will be called. Inside of this event handler, we use object destructuring to unpack the target property from our event object, then we use object destructuring again to unpack the name and value properties from the target object.


 Inside of our state setter callback function, we wrap our curly brackets in parentheses like so: setFormState((prev) => ({ ...prev })). This tells JavaScript that our curly brackets refer to a new object to be returned. We use ..., the spread operator, to fill in the corresponding fields from our previous state. Finally, we overwrite the appropriate key with its updated value. Did you notice the square brackets around the **name?** This Computed Property Name allows us to **use the string value stored by the name variable as a property key**!


---
## Separate Hooks for Separate States

[multiple State Hooks for managing separate data.](https://reactjs.org/docs/hooks-state.html#tip-using-multiple-state-variables)

 While there are times when it can be helpful to store related data in a data collection like an array or object, it can also be helpful to separate data that changes separately into completely different state variables. Managing dynamic data is much easier when we keep our data models as simple as possible.

  We can make more than one call to the State Hook. In fact, we can make as many calls to useState() as we want! It’s best to split state into multiple state variables based on which values tend to change together. We can rewrite the previous example as follows…

```
function Subject() {
  const [currentGrade, setGrade] = useState('B');
  const [classmates, setClassmates] = useState(['Hasan', 'Sam', 'Emma']);
  const [classDetails, setClassDetails] = useState({topic: 'Math', teacher: 'Ms. Barry', room: 201});
  const [exams, setExams] = useState([{unit: 1, score: 91}, {unit: 2, score: 88}]);
  // ...
}

Managing dynamic data with separate state variables has many advantages, like making our code more simple to write, read, test, and reuse across components.

```

---

## Review

- With React, we feed static and dynamic data models to JSX to render a view to the screen

- Use Hooks to “hook into” internal component state for managing dynamic data in function components

- We employ the State Hook by using the code below:
 
     - currentState to reference the current value of state
 
     - stateSetter to reference a function used to update the value of this - state
  
     - the initialState argument to initialize the value of state for the  component’s first render

   ``` 
     const [currentState, stateSetter] = useState( initialState );
   ```
 
- Call state setters in event handlers
  
- Define simple event handlers inline with our JSX event listeners and - define complex event handlers outside of our JSX
  
- Use a state setter callback function when our next value depends on - our previous value
  
- Use arrays and objects to organize and manage related data that tends - to change together
  
- Use the spread syntax on collections of dynamic data to copy the - previous state into the next state like so: `setArrayState((prev) =>  [ ...prev ]) and setObjectState((prev) => ({ ...prev }))`
 
- Split state into multiple, simpler variables instead of throwing it all into one state object