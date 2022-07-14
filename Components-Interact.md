## A Component in a Render Function

- Render methods can also return another kind of JSX: component instances.
  
```
class OMG extends React.Component {
  render() {
    return <h1>Whooaa!</h1>;
  }
}
 
class Crazy extends React.Component {
  render() {
    return <OMG />;
  }
}

```
- In the above example, Crazy‘s render method returns an instance of the OMG component class. You could say that Crazy renders an "OMG" .

---
## import  && export

- This style of importing and exporting in JavaScript is known as “named exports.” When you use named exports, you always need to wrap your imported names in curly braces, such as:
  
```
import { faveManifestos, alsoRan } from './Manifestos';`

```

- You can export multiple things from the same file:

```

// Manifestos.js:
 
export const faveManifestos = {
  futurist: 'http://www.artype.de/Sammlung/pdf/russolo_noise.pdf',
  agile:  'https://agilemanifesto.org/iso/en/manifesto.html',
  cyborg:   'http://faculty.georgetown.edu/irvinem/theory/Haraway-CyborgManifesto-1.pdf'
};
 
export const alsoRan = 'TimeCube';
```
---

## this.props (object)
- a component can pass information to another component.

- Information that gets passed from one component to another is known as “props.”

---

## Access a Component's props

- A component’s props is an object. It holds information about that component.

- To see a component’s props object, you use the expression **this.props**. Here’s an example of this.props being used inside of a render method:

```

import React from 'react';
import ReactDOM from 'react-dom';

class PropsDisplayer extends React.Component {
  render() {

    //stringProps is equal to a stringified version of this.props.
  	const stringProps = JSON.stringify(this.props);

    return (
      <div>
        <h1>CHECK OUT MY PROPS OBJECT</h1>
        <h2>{stringProps}</h2>
      </div>
    );
  }
}

// ReactDOM.render goes here:
ReactDOM.render(
  <PropsDisplayer />,
  document.getElementById('app')

)


```

---
## Pass `props` to a Component

- Let’s say that you want to pass a component the message, "This is some top secret info.". Here’s how you could do it:
  

```
 <Example message="This is some top secret info." />
``` 

 - If you want to pass information that isn’t a string, then wrap that information in curly braces. Here’s how you would pass an array:

```
<Greeting myInfo={["top", "secret", "lol"]} />
```

- In this next example, we pass several pieces of information to `<Greeting />`. The values that aren’t strings are wrapped in curly braces:

```
<Greeting name="Frarthur" town="Flundon" age={2} haunted={false} />
```

---
## Render a Component's props
- You just passed information to a component’s **props object**!

- Here’s how to make a component display passed-in information:

  1. - Find the component class that is going to receive that information.
   
  2. - Include this.props.name-of-information in that component class’s render method’s return statement.

```
import React from 'react';
import ReactDOM from 'react-dom';

class Greeting extends React.Component {
  render() {
    //make firstName show up on the screen
    return <h1>Hi there, {this.props.firstName}!</h1>;
  }
}

ReactDOM.render(
  <Greeting firstName='Sophia' />, 
  document.getElementById('app')
);
```
---

## Pass props From Component To Component

- You have learned how to pass a prop to a component:
  
```
<Greeting firstName="Esmerelda" />
```

- You have also learned how to access and display a passed-in prop:

```
render() {
  return <h1>{this.props.firstName}</h1>;
}
```

- pass a prop from one component to another.

- props is the name of the object that stores passed-in information. this.props refers to that storage object. At the same time, each piece of passed-in information is called a prop. This means that props could refer to two pieces of passed-in information, or it could refer to the object that stores those pieces of information :(

```
//This is Greeting.js
import React from 'react';

export class Greeting extends React.Component {
  render() {
    return <h1>Hi there, {this.props.name}!</h1>;
  }
}

```


```
// this is App.js
import React from 'react';
import ReactDOM from 'react-dom';
//import the Greeting component class from ./Greeting. Remember to wrap Greeting in curly braces!
import {Greeting }from"./Greeting"

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>
          Hullo and, "Welcome to The Newzz," "On Line!"
        </h1>
          <Greeting name="Sophia"/>
        
        <article>
          Latest newzz:  where is my phone?
        </article>
      </div>
    );
  }
}

ReactDOM.render(
  <App />, 
  document.getElementById('app')
);

```

---
## handleEvent, onEvent, and this.props.onEvent

- When you pass an event handler as a prop, as you just did, there are two names that you have to choose.

 1. The first name that you have to choose is the name of the event handler itself.

 2. The second name that you have to choose is the name of the prop that you will use to pass the event handler. This is the same thing as your attribute name.


-  Here’s how the naming convention works: first, think about what type of event you are listening for. In our example, the event type was “click.”



- If you are listening for a “click” event, then you name your event handler handleClick. If you are listening for a “keyPress” event, then you name your event handler handleKeyPress:

- Your prop name should be the word on, plus your event type. If you are listening for a “click” event, then you name your prop onClick. If you are listening for a “keyPress” event, then you name your prop onKeyPress:

```
class MyClass extends React.Component {
  handleHover() {
    alert('I am an event handler.');
    alert('I will listen for a "hover" event.');
  }
 
  render() {
    return <Child onHover={this.handleHover} />;
  }
}
```

---
## this.props.children

- Every component’s props object has a property named children.

- **this.props.children will return everything in between a component’s opening and closing JSX tags**.

- So far, all of the components that you’ve seen have been self-closing tags, such as `<MyComponentClass />`. They don’t have to be! You could write `<MyComponentClass></MyComponentClass>`, and it would still work.

- this.props.children would return everything in between `<MyComponentClass> and </MyComponentClass>`.


---
## defaultProps

- You can make this happen by giving your component class a property named defaultProps:

- The defaultProps property should be equal to an object:

- Inside of this object, write properties for any default props that you’d like to set:

- If an `<Example /> `doesn’t get passed any text, then it will display “yo.”
  
```
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}
 
 // Set defaultProps equal to an object:
Example.defaultProps = { text: 'yo' }; 

```

---

## this.props Recap


- Passing a prop by giving an attribute to a component instance

- Accessing a passed-in prop via this.props.prop-name
  
- Displaying a prop
  
- Using a prop to make decisions about what to display
  
- Defining an event handler in a component class

- Passing an event handler as a prop

- Receiving a prop event handler and attaching it to an event listener
  
- Naming event handlers and event handler attributes according to convention

- this.props.children

- getDefaultProps

---

## this.state
- React components will often need dynamic information in order to render. For example, imagine a component that displays the score of a basketball game. The score of the game might change over time, meaning that the score is dynamic. Our component will have to know the score, a piece of dynamic information, in order to render in a useful way.
  
- There are two ways for a component to get dynamic information: **props and state**. Besides props and state, every value used in a component should always stay exactly the same.

---
## Setting Initial State (should be equal to an object)

- A React component can access dynamic information in two ways: props and state

- Unlike props, a component’s state is not passed in from the outside. **A component decides its own state.**

- To make a component have state, give the component a state property. This property should be declared inside of a constructor method, like this:

- this.state should be equal to an object, like in the example below. This object represents the initial “state” of any component instance.

- constructor and super are both features of ES6, not unique to React. 

- It is important to note that React components always have to call **super in their constructors**to be set up properly.


- Look at the bottom of the highest code example in this column. `<Example />` has a state, and its state is equal to { mood: 'decent' }.
  
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }
 
  render() {
    return <div></div>;
  }
}
 
<Example />
```

- Another example:

```
import React from 'react';
import ReactDOM from 'react-dom';

class App extends React.Component {
	// constructor method begins here:
constructor(props){
  super(props)
    this.state={ title: 'Best App' };
}
  render() {
    return (
      <h1>
        Wow this entire app is just an h1.
      </h1>
    );
  }
}
```

---

## Access a Component's state

- To read a component’s state, use the expression this.state.name-of-property:
  
- Just like this.props, you can use this.state from any property defined inside of a component class’s body.
  
```
class TodayImFeeling extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }
 
  render() {
    return (
      <h1>
        I'm feeling {this.state.mood}!
      </h1>
    );
  }
}
```
---

## Update state with this.setState

- A component can do more than just read its own state. A component can also change its own state.

- A component changes its state by calling the function this.setState().

- this.setState() **takes two arguments**: **an object** that will update the component’s state, and **a callback**. You basically never need the callback.

---

## Call this.setState from Another Function

- The most common way to call this.setState() is to call a custom function that wraps a this.setState() call. .makeSomeFog() is an example:

- Notice how the method makeSomeFog() contains a call to this.setState().

- [The bind() method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind) creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

- We need to bind these methods to the component instance using .bind() in our custom component’s constructor.
  
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = { weather: 'sunny' };

    //This line is necessary because makeSomeFog()‘s body contains the word this. 
    this.makeSomeFog = this.makeSomeFog.bind(this);
  }
 
 //the method
  makeSomeFog() {
    this.setState({
      weather: 'foggy'
    });
  }
}
```

### **Change Color example**

- If you call .changeColor(), shouldn’t you then also have to call .render() again?

- Any time that you call this.setState(), this.setState() AUTOMATICALLY calls .render() as soon as the state has changed.

- Think of this.setState() as actually being two things: this.setState(), immediately followed by .render().

- That is why you can’t call this.setState() from inside of the .render() method! this.setState() automatically calls .render(). If .render() calls this.setState(), then an infinite loop is created.


```
//Toggle.js
const green = '#39D1B4';
const yellow = '#FFD712';

class Toggle extends React.Component {
  constructor(props){
    super(props)
    this.state= { color: green };

    //When you write a component class method that uses this, then you need to bind that method inside of your constructor function!
   this.changeColor = this.changeColor.bind(this);
  }

  //method
  changeColor(){

    const newColor = this.state.color == green ? yellow : green ;
    this.setState({ color: newColor });
  }

  render() {
    return (
      <div style={{background: this.state.color}}>
        <h1>
          Change my color
          <button onClick={this.changeColor}>
          Change color
         </button>
        </h1>
      </div>
    );
  }
}
```


```
//Mood.js
import React from 'react';
import ReactDOM from 'react-dom';

class Mood extends React.Component {
  constructor(props) {
    super(props);
    this.state = { mood: 'good' };
    this.toggleMood = this.toggleMood.bind(this);
  }

  toggleMood() {
    const newMood = this.state.mood == 'good' ? 'bad' : 'good';
    this.setState({ mood: newMood });
  }

  render() {
    return (
      <div>
        <h1>I'm feeling {this.state.mood}!</h1>

        //make the button actually work!
        <button onClick={this.toggleMood}>
          Click Me
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Mood />, document.getElementById('app'));
```


