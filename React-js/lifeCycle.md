# Component Life cycle

to understand the component life cycle check [the lifecycle diagrame](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

---

## `componentDidMount` Method

Most web developers, at some point, need to call an API endpoint to retrieve data. 

The best practice with React is to place API calls or any calls to your server in the lifecycle method **`componentDidMount()`**. 

This method is called after a component is mounted to the DOM. Any calls to `setState()` here will trigger a re-rendering of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

```
class LifeCycle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      time: new Date()
    };
  }

  componentDidMount() {
    setInterval( () => {
      this.setState({
        time: new Date()
      });
    }, 1000);
  }

  render() {
    return (
      <div>
        <h1>
            Clock: { this.state.time.toLocaleTimeString() }
        </h1>
      </div>
    );
  }
};
```

---

## Add Event Listeners

The **`componentDidMount()`** method is also the best place to attach any event listeners you need to add for specific functionality. 

in **`componentWillUnmount()`**, remove this same event listener. You can pass the same arguments to document.`removeEventListener()`. 

It's good practice to use this lifecycle method to do any clean up on React components before they are unmounted and destroyed. Removing event listeners is an example of one such clean up action.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
    this.handleSpace = this.handleSpace.bind(this);
  }

  componentDidMount() {
    document.addEventListener('keydown', this.handleKeyPress)
  }

  componentWillUnmount() {
    document.removeEventListener('keydown', this.handleKeyPress)
  }

  handleSpace() {
    this.setState({
      message: ''
    });
  }

  handleEnter() {
    this.setState({
      message: this.state.message + 'You pressed the enter key! '
    });
  }

  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
    if (event.keyCode === 32) {
      this.handleSpace();
    }
  }

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```

---

## Optimize Re-Renders with `shouldComponentUpdate`

if any component receives new state or new props, it re-renders itself and all its children.

But React provides a lifecycle method you can call when child components receive new state or props, and declare specifically if the components should update or not. 

The method is **`shouldComponentUpdate()`**, and it takes nextProps and nextState as parameters.

This method is a useful way to optimize performance. For example, the default behavior is that your component re-renders when it receives new props, even if the props haven't changed. You can use **`shouldComponentUpdate()`** to prevent this by comparing the props. 

The method must `return a boolean value` that tells React whether or not to update the component. You can compare the current props (this.props) to the next props (nextProps) to determine if you need to update or not, and return true or false accordingly.

```
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    if(nextProps.value % 2 == 0){
      return true;
    }
    return false;
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>
  }
};

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState({
      value: this.state.value + 1
    });
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value}/>
      </div>
    );
  }
};
```

previous: [Component with State](StatefulComponent.md)

Next: [Forms](form.md)