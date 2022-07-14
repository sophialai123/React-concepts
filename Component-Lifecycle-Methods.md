## Introduction to Lifecycle Methods

- React components have several methods, called lifecycle methods, that are called at different parts of a component’s lifecycle. This is how you, the programmer, deal with the lifecycle of a component.

- You may not have known it, but you’ve already used two of the most common lifecycle methods: constructor() and render()! constructor() is the first method called during the mounting phase. render() is called later during the mounting phase, to render the component for the first time, and during the updating phase, to re-render the component.


- Notice that lifecycle methods don’t necessarily correspond one-to-one with part of the lifecycle. constructor() only executes during the mounting phase, but render() executes during both the mounting and updating phase.


---

## componentDidMount

the component lifecycle has three high-level parts:

  1. Mounting, when the component is being initialized and put into the DOM for the first time
  2. Updating, when the component updates as a result of changed state or changed props
  3. Unmounting, when the component is being removed from the DOM

componentDidMount() is the final method called during the mounting phase. The order is:

 1. The constructor
 2. render()
 3. componentDidMount()

```
import React from 'react';
import ReactDOM from 'react-dom';

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }
  render() {
    return <div>{this.state.date.toLocaleTimeString()}</div>;
  }
 
 // updated the clock every second
  componentDidMount() {
    const oneSecond = 1000;
setInterval(() => {
  this.setState({ date: new Date() });
}, oneSecond);
  }
}

ReactDOM.render(<Clock />, document.getElementById('app'));

```
---
## componentWillUnmount 

Let’s introduce a new lifecycle method: componentWillUnmount(). componentWillUnmount() is called in the unmounting phase, right before the component is completely destroyed. **It’s a useful time to clean up any of your component’s mess**.

```
import React from 'react';

export class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }
  render() {
    return <div>{this.state.date.toLocaleTimeString()}</div>;
  }
  componentDidMount() {
    const oneSecond = 1000;
    this.intervalID =setInterval(() => {
      this.setState({ date: new Date() });
    }, oneSecond);
  }

   //clear up a side-effect
  componentWillUnmount(){
    clearInterval(this.intervalID)
  }
}
```

---
## componentDidUpdate

Remember the three parts of a component’s lifecycle:

 1. Mounting, when the component is being initialized and put into the DOM for the first time. We’ve looked at mounting (constructor(), render(), and componentDidMount()). 
   
 2. Updating, when the component updates as a result of changed state or changed props.componentDidUpdate()

 
 3. Unmounting, when the component is being removed from the DOM. We’ve looked at unmounting (componentWillUnmount()).

An update is caused by changes to props or state. You’ve already seen this happen a bunch of times. Every time you’ve called setState() with new data, you’ve triggered an update. Every time you change the props passed to a component, you’ve caused it to update.


When a component updates, it calls [several methods](https://reactjs.org/docs/react-component.html#updating), but only two are commonly used.


1. The first is render(), which we’ve seen in every React component. When a component’s props or state changes, render() is called.

 
2. The second is componentDidUpdate(). Just like componentDidMount() is a good place for mount-phase setup, componentDidUpdate() is a good place for update-phase work.


```
```
```
```
```
```