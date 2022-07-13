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