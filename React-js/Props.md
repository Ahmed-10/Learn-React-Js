# Props

In React, you can pass props, or properties, to child components. 

Say you have an `App` component which renders a child component called `Welcome` which is a stateless functional component. 

You can pass Welcome a user property by writing:
```
<App>
  <Welcome user='Mark' />
</App>
```
In this case, the created property user is passed to the component Welcome. 

Since Welcome is a stateless functional component, it has access to this value like so:
```
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```

---
## Pass an Array as Props

```
const List = (props) => {
  return (<p>{props.tasks.join(", ")}</p>);
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        <List tasks={["Walk", "Cook", "Bake"]} />
        <h2>Tomorrow</h2>
        <List tasks={["Study", "Code", "Eat"]} />
      </div>
    );
  }
};

```
---
## Default Props

React also has an option to set default props. 

You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. 

This allows you to specify what a prop value should be if no value is explicitly provided.

to override the default props is to explicitly set the prop values for a component.

```
 const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity={50}/>
  }
};
```
---
## Define props PropTypes

React provides useful type-checking features to verify that components receive props of the correct type.

You can set propTypes on your component to require the data to be of type `array`. This will throw a useful warning when the data is of any other type.

```
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

Items.propTypes = {
  quantity: PropTypes.number.isRequired
};

Items.defaultProps = {
  quantity: 0
};

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items />
  }
};
```
---
## Access Props Using this.prop

if the child component that you're passing a prop to is an ES6 class component

you use the **`this`** keyword. 

For example, if an ES6 class component has a prop called data, you write **`{this.props.data}`** in JSX.

```
class ReturnTempPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
            <p>
                Your temporary password is: <strong>{this.props.tempPassword}</strong>
            </p>
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
        <div>
          <h2>Reset Password</h2>
          <h3>We've generated a new temporary password for you.</h3>
          <h3>Please reset this password from your account settings ASAP.</h3>
          <ReturnTempPassword tempPassword="xxxxxxxx"/>
        </div>
    );
  }
};
```
---
previous: [React Components](ReactComponent.md)

Next: [Component with State](StatefulComponent.md)