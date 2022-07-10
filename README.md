# INTRO TO JSX

## JSX Elements
- JSX elements are treated as JavaScript expressions. They can go anywhere that JavaScript expressions can go.
  
- That means that a JSX element can be saved in a variable, passed to a function, stored in an object or array…you name it.

- Here’s an example of several JSX elements being stored in an object:
```
const myTeam = {
  center: <li>Benzo Walli</li>,
  powerForward: <li>Rasha Loa</li>,
  smallForward: <li>Tayshaun Dasmoto</li>,
  shootingGuard: <li>Colmar Cumberbatch</li>,
  pointGuard: <li>Femi Billon</li>
};

```

---
## Attributes In JSX

- A JSX attribute is written using HTML-like syntax: a name, followed by an equals sign, followed by a value. The value should be wrapped in quotes, like this:

```
//JSX element can have many attributes,
const panda = <img src='images/panda.jpg' alt='panda' width='500px' height='500px' />;

```
---
## Nested JSX
- You can nest JSX elements inside of other JSX elements, just like in HTML.

```
<a href="https://www.example.com">
  <h1>
    Click me!
  </h1>
</a>
```

- If a JSX expression takes up more than one line, then you must wrap the multi-line JSX expression in parentheses
  
- Nested JSX expressions can be saved as variables, passed to functions, etc., just like non-nested JSX expressions can! Here’s an example of a nested JSX expression being saved as a variable:
  
```
 const theExample = (
   <a href="https://www.example.com">
     <h1>
       Click me!
     </h1>
   </a>
 );
```

---
## JSX Outer Elements

- There’s a rule that we haven’t mentioned: a JSX expression must have exactly one outermost element, wrap the JSX expression in a "div".

```
//all the element inside of the div
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```
---
## Rendering JSX
- To render a JSX expression means to make it appear onscreen.
  
- JavaScript is case-sensitive, so make sure to capitalize ReactDOM correctly!
  
```
ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```
---
## ReactDOM.render() 

- ReactDOM is the name of a JavaScript library. This library contains several React-specific methods, all of which deal with the [DOM](https://www.w3schools.com/js/js_htmldom.asp) in some way or another.

- ReactDOM.render() is the most common way to render JSX. It takes a JSX expression, creates a corresponding tree of DOM nodes, and adds that tree to the DOM. That is the way to make a JSX expression appear onscreen.

```
import React from 'react';
import ReactDOM from 'react-dom';

// This is just an example, switch to app.js for the exercise.
ReactDOM.render(<h1>Render me!</h1>, document.getElementById('app'));

```
---

## Passing a Variable to ReactDOM.render()

- ReactDOM.render()‘s first argument should evaluate to a JSX expression, it doesn’t have to literally be a JSX expression.
  
- The first argument could also be a variable, so long as that variable evaluates to a JSX expression.

- Save a JSX expression as a variable named toDoList. We then pass toDoList as the first argument to ReactDOM.render():

```
const toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);
 
ReactDOM.render(
  toDoList, 
  document.getElementById('app')
);
```

---
## The Virtual DOM

- One special thing about ReactDOM.render() is that it only updates DOM elements that have changed.

- That means that if you render the exact same thing twice in a row, the second render will do nothing:

```
const hello = <h1>Hello world</h1>;
 
// This will add "Hello world" to the screen:
ReactDOM.render(hello, document.getElementById('app'));
 

// This won't do anything at all:
ReactDOM.render(hello, document.getElementById('app'));
```

--- 

# ADVANCED JSX

## class vs className
- When JSX is rendered, JSX className attributes are automatically rendered as class attributes.

```
//In HTML, it’s common to use class
<h1 class="big">Hey</h1>

//In JSX,use className
<h1 className="big">Hey</h1>
```
---
## Self-Closing Tags
- In JSX, you have to include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error:

```
  <br />
  <img /> 
```
---
## JavaScript In Your JSX In Your JavaScript

```
import React from 'react';
import ReactDOM from 'react-dom';

// Write code here:
ReactDOM.render(
  <h1>2 + 3</h1>,
  document.getElementById('app')
);

//Output:
2 + 3
```

---
## Curly Braces in JSX
- Any code in between the tags of a JSX element will be read as JSX, not as regular JavaScript! JSX doesn’t add numbers - it reads them as text, just like HTML.

- You can do this by wrapping your code in curly braces.

```
import React from 'react';
import ReactDOM from 'react-dom';

// Write code here:
ReactDOM.render(
  <h1>{2 + 3}</h1>,
  document.getElementById('app')
);

//Output:
5

```

---
## Variables in JSX
- When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.
  
- That means that you can access variables while inside of a JSX expression, even if those variables were declared on the outside.

```
// Declare a variable:
const name = 'Gerdo';
 
// Access your variable 
// from inside of a JSX expression:
const greeting = <p>Hello, {name}!</p>;

```
---

## Variable Attributes in JSX
- When writing JSX, it’s common to use variables to set attributes.

```

// Use a variable to set the `height` and `width` attributes:
 
const sideLength = "200px";
 
const panda = (
  <img 
    src="images/panda.jpg" 
    alt="panda" 
    height={sideLength} 
    width={sideLength} />
);

```

- Object properties are also often used to set attributes:

```
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
}; 
 
const panda = (
  <img 
    src={pics.panda} 
    alt="Lazy Panda" />
);
 
const owl = (
  <img 
    src={pics.owl} 
    alt="Unimpressed Owl" />
);
 
const owlCat = (
  <img 
    src={pics.owlCat} 
    alt="Ghastly Abomination" />
); 
```
---

## Event Listeners in JSX
- Create an event listener by giving a JSX element a special attribute. 
  
- An event listener attribute’s name should be something like onClick or onMouseOver: the word on, plus the type of event that you’re listening for. You can see a list of valid event names [here](https://reactjs.org/docs/events.html#supported-events).

- An event listener attribute’s value should be a function. The above example would only work if myFunc were a valid function that had been defined elsewhere:

```
function myFunc() {
  alert('Make myFunc the pFunc... omg that was horrible i am so sorry');
}
 
<img onClick={myFunc} />
```

- Note that in HTML, event listener names are written in all lowercase, such as onclick or onmouseover. In JSX, event listener names are written in camelCase, such as onClick or onMouseOver.