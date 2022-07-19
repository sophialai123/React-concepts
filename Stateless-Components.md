# Stateless Components Inherit From Stateful Components

Our programming pattern uses two React components: a stateful component, and a stateless component. “Stateful” describes any component that has a state property; “stateless” describes any component that does not.


In our pattern, a stateful component passes its state down to a stateless component.

---

## Build a Stateful Component Class

To make that happen, you need two component classes: a stateful class, and a stateless class.


1. a stateful component class named Parent.
```

import React from "react";
import ReactDOM from "react-dom";

//Parent will represent your stateful component class.
class Parent extends React.Component{
  constructor(props){
    super(props);
    this.state={name:"Frarthur"}
  }
  render(){
    return <div></div>;
  }
}

```


---
## Build a Stateless Component Class

2. make our stateless component class named Child

```
import React from "react";
//Child will represent your stateless component class.
export class Child extends React.Component{
  render(){

    //Child is going to receive a prop called name, and display that prop on the screen.

    return <h1>Hey, my name is {this.props.name}!</h1>
  }
}
```

---
## Pass a Component's State

```
import React from "react";
import ReactDOM from "react-dom";
import {Child} from './Child'

//Parent will represent your stateful component class.
class Parent extends React.Component{
  constructor(props){
    super(props);
    this.state={name:"Frarthur"}
  }
  render(){

    //render Child component and pass a prop
    return <Child  name={this.state.name}/>;
  }
}

ReactDOM.render(<Parent />,
document.getElementById('app'));
```

---

## Child Components Update Their Parents' state

How does a stateless, child component update the state of the parent component? Here’s how that works:

1. The parent component class defines a method that calls this.setState(). For an example, at the .handleClick() method.

2. The parent component binds the newly-defined method to the current instance of the component in its constructor. This ensures that when we pass the method to the child component, it will still update the parent component. For an example,  at the end of the constructor() method.

3. Once the parent has defined a method that updates its state and bound to it, the parent then passes that method down to a child. Look  at the prop.

4. The child receives the passed-down function, and uses it as an event handler. When a user clicks on the `<button></button>`, a click event will fire. This will make the passed-down function get called, which will update the parent’s state.


### ParentClass

```
import React from 'react';
import ReactDOM from 'react-dom';
import { ChildClass } from './ChildClass';

class ParentClass extends React.Component {
  constructor(props) {
    super(props);

    this.state = { totalClicks: 0 };

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    const total = this.state.totalClicks;

    // calling handleClick will 
    // result in a state change:
    this.setState(
      { totalClicks: total + 1 }
    );
  }

  // The stateful component class passes down
  // handleClick to a stateless component class:
  render() {
    return (
      <ChildClass onClick={this.handleClick} />
    );
  }
}
```
### ChildClass

```
import React from 'react';
import ReactDOM from 'react-dom';

export class ChildClass extends React.Component {
  render() {
    return (
      // The stateless component class uses
      // the passed-down handleClick function,
      // accessed here as this.props.onClick,
      // as an event handler:
      <button onClick={this.props.onClick}>
        Click Me!
      </button>
    );
  }
}
```

---
### Define an Event Handler

To make a child component update its parent’s state, the first step is something that you’ve seen before: you must define **a state-changing method on the parent**.

### Pass the Event Handler

Defined a function in Parent that can change Parent‘s state.

Parent must pass this function down to Child, so that Child can use it in an event listener on the dropdown menu.

### Receive the Event Handler

Parent class

```
import React from 'react';
import ReactDOM from 'react-dom';
import { Child } from './Child';

class Parent extends React.Component {
  constructor(props) {
    super(props);

    this.state = { name: 'Frarthur' };
    
    this.changeName = this.changeName.bind(this);
  }
  
  changeName(newName) {
    this.setState({
      name: newName
    });
  }

  render() {
    return <Child name={this.state.name} onChange={this.changeName} />
  }
}

ReactDOM.render(
	<Parent />,
	document.getElementById('app')
);
```


Child class

```
import React from 'react';

export class Child extends React.Component {
  constructor(props) {
    super(props);
    
    this.handleChange = this.handleChange.bind(this);
  }
  
  //define another function change names
  handleChange(e) {
    const name = e.target.value;
    this.props.onChange(name);
  }

  render() {
    return (
      <div>
        <h1>
          Hey my name is {this.props.name}!
        </h1>

        //create an event listener
        <select id="great-names" onChange={this.handleChange}>
          <option value="Frarthur">
            Frarthur
          </option>

          <option value="Gromulus">
            Gromulus
          </option>

          <option value="Thinkpiece">
            Thinkpiece
          </option>
        </select>
      </div>
    );
  }
}
```

---
## Child Components Update Sibling Components

### One Sibling to Display, Another to Change

You should divide Child in two: one component for displaying the name, and a different component for allowing a user to change the name.

### Pass the Right props to the Right Siblings
