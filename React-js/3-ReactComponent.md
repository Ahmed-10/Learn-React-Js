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