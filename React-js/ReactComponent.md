# React Component

Components are the core of React. Everything in React is a component.

---
## stateless functional component

There are two ways to create a React component. The first way is to use a JavaScript function. Defining a component in this way creates *a stateless functional component*.

```
const MyComponent = function() {
  return (
    <div>
        Hello a stateless functional component
    </div>
  )
}
```

---
## Create React component

The other way to define a React component is with the ES6 class syntax. 

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
        <div>
            <h1>Hello React!</h1>
        </div>
    );
  }
};
```

This creates an ES6 class *`MyComponent`* which extends the *`React.Component`* class. So the *`MyComponent`* class now has access to many useful React features, such as 
* local state 
* lifecycle hooks. 

the *`MyComponent`* class has a constructor defined within it that calls `super()`. 

It uses `super()` to call the constructor of the parent class, in this case *`React.Component`*. 

The constructor is a special method used during the initialization of objects that are created with the class keyword. It is best practice to call a component's constructor with super. This makes sure the component is initialized properly. For now, It is standard for this code to be included.

---
##  Create a Component with Composition

To compose multiple React components together, you could create an App parent component which renders each of these three components as children. 

To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX.

```
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1>
        <ChildComponent />
      </div>
    );
  }
};
```
---
## Render a Class Component to the DOM

none of the React code you write will render to the DOM without making a call to the ReactDOM API.

a refresher on the syntax: 
**`ReactDOM.render(componentToRender, targetNode)`**. 

The first argument is the React component that you want to render. The second argument is the DOM node that you want to render that component within.

```
ReactDOM.render(<MyComponent />, document.getElementById("root"));
```
---
previous: [JSX extension](JSX_Syntax.md)

Next: [Props](Props.md)