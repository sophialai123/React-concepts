## Class Components

- This code will create and render a new React component:
  
```
import React from 'react';
import ReactDOM from 'react-dom';
 
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
};
 
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);
```

- This creates an object named React which contains methods necessary to use the React library.
  
```
import React from 'react';
```

- The methods imported from 'react-dom' are meant for interacting with the DOM. You are already familiar with one of them: ReactDOM.render().

```
import ReactDOM from 'react-dom';
```
---

## Create a Component Class

- All class components will have some methods and properties in common (more on this later). Rather than rewriting those same properties over and over again every time, we extend the Component class from the React library. This way, we can use code that we import from the React library, without having to write it over and over again ourselves.

- After we define our class component, we can use it to render as many instances of that component as we want.

- React.Component is a JavaScript class. To create your own component class, you must subclass React.Component. You can do this by using the syntax class YourComponentNameGoesHere extends React.Component {}.

- Take another look at the code from the first exercise:

```
import React from 'react';
import ReactDOM from 'react-dom';
 

 //declaring a new component class,
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
 
ReactDOM.render(
    <MyComponentClass />, 
    document.getElementById('app')
);

```

---
## Name a Component Class
- Subclassing React.Component is the way to declare a new component class.

- Component class variable names must begin with **capital letters**!

---

## Component Class Instructions

   1. import React from 'react' creates a JavaScript object. This object contains properties that are needed to make React work, such as React.createElement() and React.Component.
   
   2. import ReactDOM from 'react-dom' creates another JavaScript object. This object contains methods that help React interact with the DOM, such as ReactDOM.render().

   3. by subclassing React.Component, you create a new component class. This is not a component! **A component class is more like a factory that produces components**. When you start making components, each one will come from a component class.
   
   4. Whenever you create a component class, you need to give that component class a name. That name should be written in UpperCamelCase. In this case, your chosen name is MyComponentClass.

---
## The Render Function

- A component class is like a factory that builds components. It builds these components by consulting a set of instructions, which you must provide. Let’s talk about these instructions!

- For starters, these instructions should take the form of a class declaration body. That means that they will be delimited by curly braces, like this:
  

```
class ComponentFactory extends React.Component {
  // instructions go here, between the curly braces
}
```

- A render method is a property whose name is render, and whose value is a function. The term “render method” **can refer to the entire property, or to just the function part.**

- A render method must contain a return statement. Usually, this return statement returns a JSX expression:
  
```
class ComponentFactory extends React.Component {

  render() {
    return <h1>Hello world</h1>;
  }
}

```

## Create a Component Instance

- MyComponentClass is now a working component class! It’s ready to follow its instructions and make some React components.
  
- JSX elements can be either HTML-like, or component instances. JSX uses **capitalization** to distinguish between the two! That is the React-specific reason **why component class names must begin with capital letters**. In a JSX element, that capitalized first letter says, “I will be a component instance and not an HTML tag.”

```
// create an instance of MyComponentClass.
<MyComponentClass />
```

---

## Render A Component

- You have learned that a component class needs a set of instructions, which tell the component class how to build components. When you make a new component class, these instructions are the body of your class declaration:

```
class MyComponentClass extends React.Component
{ // everything in between these curly-braces is instructions for how to build components
 

 //has one method, named render
  render() {
    return <h1>Hello world</h1>;
  }
}

```

- Whenever you make a component, that component inherits all of the methods of its component class. MyComponentClass has one method: MyComponentClass.render(). Therefore, <MyComponentClass /> also has a method named render.


- You could make a million different <MyComponentClass /> instances, and each one would inherit this same exact render method.

- To call a component’s render method, you pass that component to ReactDOM.render(). Notice your component, being passed as ReactDOM.render()‘s first argument:

```
ReactDOM.render(
  <MyComponentClass />,
  document.getElementById('app')
);

```

---
## Use Multiline JSX in a Component
- A multi-line JSX expression should always be wrapped in parentheses

---

## Use a Variable Attribute in a Component
- Take a look at this JavaScript object named redPanda:

```
import React from 'react';
import ReactDOM from 'react-dom';

const redPanda = {
  src: 'https://upload.wikimedia.org/wikipedia/commons/b/b2/Endangered_Red_Panda.jpg',
  alt: 'Red Panda',
  width:  '200px'
};

class RedPanda extends React.Component {
  render() {
    return (
      <div>
        <h1>Cute Red Panda</h1>
        <img 
          src={redPanda.src}
          alt={redPanda.alt}
          width={redPanda.width} />
      </div>
    );
  }
}

ReactDOM.render(
  <RedPanda />,
  document.getElementById('app')
);

```

---

## Put Logic in a Render Function

- A render() function must have a return statement. However, that isn’t all that it can have.

- A render() function can also be a fine place to put simple calculations that need to happen right before a component renders. Here’s an example of some calculations inside of a render function:

```

class Random extends React.Component {
  render() {
    // First, some logic that must happen
    // before rendering:
    const n = Math.floor(Math.random() * 10 + 1);


    // Next, a return statement
    // using that logic:
    return <h1>The number is {n}!</h1>;
  }
}

```


- Another example:

```

import ReactDOM from "react-dom"
import React from "react"


const friends = [
  {
    title: "Yummmmmmm",
    src: "https://content.codecademy.com/courses/React/react_photo-monkeyweirdo.jpg"
  },
  {
    title: "Hey Guys!  Wait Up!",
    src: "https://content.codecademy.com/courses/React/react_photo-earnestfrog.jpg"
  },
  {
    title: "Yikes",
    src: "https://content.codecademy.com/courses/React/react_photo-alpaca.jpg"
  }
];

// New component class starts here:
class Friend extends React.Component{
  render(){
    const friend = friends [0];
    return (
       <div>
       <h1>{friend.title}</h1>
       <img  
       src= {friend.src}
       />
    </div>
    )
  }
}


ReactDOM.render(<Friend/>,
document.getElementById('app')

)
```
---

## Use a Conditional in a Render Function
 - Notice that the if statement is located inside of the render function, but before the return statement. This is pretty much the only way that you will ever see an if statement used in a render function.

```

import React from 'react';
import ReactDOM from 'react-dom';

const fiftyFifty = Math.random() < 0.5;

// New component class starts here:
class TonightsPlan extends React.Component{
  render(){
    if(fiftyFifty){
      return <h1>Tonight I'm going out WOOO</h1>
    }else{
      <h1>Tonight I'm going to bed WOOO</h1>
    }
  }
}

ReactDOM.render(
     <TonightsPlan />,
   	document.getElementById('app')
);
```

---

## [Use this in a Component](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)
- You are especially likely to see this inside of the body of a component class declaration. Here’s an example:

```
class IceCreamGuy extends React.Component {

  //two methods
  get food() {
    return 'ice cream';
  }
 
  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```

- this refers to an instance of IceCreamGuy. The less simple answer is that this refers to the object on which this‘s enclosing method, in this case .render(), is called. It is almost inevitable that this object will be an instance of IceCreamGuy, but technically it could be something else.

- Let’s assume that this refers to an instance of your component class, as will be the case in all examples in this course.**IceCreamGuy has two methods: .food and .render().** Since this will evaluate to an instance of IceCreamGuy, this.food will evaluate to a call of IceCreamGuy‘s .food method. This method will, in turn, evaluate to the string “ice cream.”

- You don’t need those parentheses because .food is a getter method. You can tell this from the get in the above class declaration body.
  
- There’s nothing React-specific about getter methods, nor about this behaving in this way!



- Another example
```
import React from 'react';
import ReactDOM from 'react-dom';

class MyName extends React.Component {
	// name property goes here:
get name(){
  return 'Sophia';
}

  render() {
    return <h1>My name is {this.name}.</h1>;
  }
}

ReactDOM.render(<MyName />, document.getElementById('app'));

```
---
## Use an Event Listener in a Component
- Render functions often contain event listeners. 

- In React, you define event handlers as methods on a component class. Like this:

```
class MyClass extends React.Component {
  myFunc() {
    alert('Stop it.  Stop hovering.');
  }
 
  render() {
    return (
      <div onHover={this.myFunc}>
      </div>
    );
  }
}
```
- Notice that the component class has two methods: .myFunc() and .render(). **.myFunc() is being used as an event handler**. .myFunc() will be called any time that a user hovers over the rendered 'div'.
  