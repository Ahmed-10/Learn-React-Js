# JSX extension
React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. This has several benefits. It lets you use the full programmatic power of JavaScript within HTML, and helps to keep your code readable. For the most part, JSX is similar to the HTML

```
const JSX = <h1>Hello JSX!</h1>;

ReactDOM.render(JSX, document.getElementById('root'))
```
---
## add comment in JSX

To put comments inside JSX, you use the syntax {/* */} to wrap around the comment text.

```
const JSX = (
  <div>
    <h1>This is a block of JSX</h1>
    { /*this comment will not be rendered */}
    <p>Here's a subtitle</p>
  </div>
);
```

---
## Define an HTML Class in JSX

One key difference in JSX is that you can no longer use the word class to define HTML classes. This is because class is a reserved word in JavaScript. Instead, JSX uses className.

```
const JSX = (
  <div className='style-class'>
    <h1>This is a block of JSX</h1>
    <p>Here's a subtitle</p>
  </div>
);
```
---
## Self-Closing Tags

 Any JSX element can be written with a self-closing tag, and every element must be closed. The line-break tag, for example, must always be written as ` <br /> ` in order to be valid JSX that can be transpiled. 
 
 A `<div>`, on the other hand, can be written as `<div />` or `<div></div>`. The difference is that in the first syntax version there is no way to include anything in the `<div />`. 

```
 const JSX = (
  <div>
    <h2>Welcome to React!</h2> <br />
    <p>Be sure to close all tags!</p>        
  </div>
);
```
---
previous: [Getting started](GettingStarted.md)

Next: [React Components](ReactComponent.md)