# Component with State

One of the most important topics in React is state. 

State consists of any data your application needs to know about, that can change over time. 

You want your apps to respond to state changes and present an updated UI when necessary.

You create state in a React component by declaring a **`state`** property on the component **`class`** in its **`constructor`**. This initializes the component with state when it is created. 

**The `state` property must be set to a JavaScript `object`.**

```
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    // initialize state
    this.state = {
      name: 'React'
    }
  }
  render() {
    return (
      <div>
        <h1>Hello {this.state.name}!</h1>
      </div>
    );
  }
};
```

If a component is stateful, it will always have access to the data in `state` in its `render()` method. You can access the data with `this.state`.

Note that if you make a component stateful, no other components are aware of its state. Its state is completely encapsulated, or local to that component, unless you pass state data to a child component as props.

---
## set state

There is also a way to change the component's state. React provides a method for updating component state called `setState`.

call the `setState` method within your component class like so: `this.setState()`, passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({
      name: 'React Rocks!'
    })
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```
A class method `handleClick` typically needs to use the `this` keyword so it can access properties on the class (such as `state` and `props`) inside the scope of the method. 

One common way is to explicitly bind this in the constructor so this becomes bound to the class methods when the component is initialized. 

we used **`this.handleClick = this.handleClick.bind(this)`** for this `handleClick` method in the constructor. 

Then, when you call a function like `this.setState()` within your class method.

---

## Toggle state

Sometimes you might need to know the previous state when updating the state. However, state updates may be asynchronous - this means React may batch multiple `setState()` calls into a single update. This means you can't rely on the previous value of `this.state` or `this.props` when calculating the next value.

you should pass `setState` a function that allows you to access state and props. Using a function with `setState` guarantees you are working with the most current values of `state` and `props`.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };

    this.toggleVisibility = this.toggleVisibility.bind(this);
  }

  toggleVisibility(){
    this.setState(state => ({
      visibility: !(state.visibility)
    }))
  }

  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
};
```
---

## Pass State as Props to Child Components

```
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Ahmed'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={ this.state.name} />
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is: { this.props.name } </h1>
    </div>
    );
  }
};
```
---

## Pass a Callback as Props

You can pass handler functions or any method that's defined on a React component to a child component. 

This is how you allow child components to interact with their parent components. 

You pass methods to a child just like a regular prop. It's assigned a name and you have access to that method name under `this.props` in the child component.

```
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        <GetInput 
          input={ this.state.inputValue}
          handleChange={ this.handleChange} />

        <RenderInput input={ this.state.inputValue }/>
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```
---

## exercise

The Counter component keeps track of a count value in state. There are two buttons which call methods `increment()`, `decrement()`, and `reset()`. 

The counter value is incremented or decremented by 1 when the appropriate button is clicked. Also, when the reset button is clicked, the count is set to 0.


```
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };

    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
    this.reset = this.reset.bind(this);
  }

  increment(){
    this.setState(state => ({
      count: state.count +1
    }))
  }

  decrement(){
    this.setState(state => ({
      count: state.count -1
    }))
  }

  reset(){
    this.setState({
      count: 0
    })
  }

  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```
---

previous: [Props](Props.md)

Next: [Component life cycle](lifeCycle.md)