# Add React to a Website 

1. In terminal
```
>> Run npm init -y 
 
//to add babel command line interface, babel-preset-react-app to node_modules
>> Run npm install babel-cli@6 babel-preset-react-app@3 
```

2. In the html file we add
    <!-- ... React container -->
    <div id="root"></div>
 
    <!-- Load React. -->
    <!-- Note: when deploying, replace "development.js" with "production.min.js". -->
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    
    <!-- Load our React component. -->
    <script src="main.js"></script>
</body>

3. Create folder in the project directory “src”

4. Create main.js in the src folder and add the following

```
var app = <div>Hello React World!</div>

root = document.getElementById('root')
    
ReactDOM.render(app, root)
```

5. In the terminal
```
>> npx babel --watch src --out-dir . --presets react-app/prod
```

If you now create a file called src/main.js with this JSX starter code, the babel watcher will create a preprocessed main.js with the plain JavaScript code suitable for the browser. When you edit the source file with JSX, the transform will re-run automatically.

# Create a New React App

for more details check [create a new react app](https://reactjs.org/docs/create-a-new-react-app.html) 

## Recommended Toolchains

If you’re learning React or creating a new single-page app, use Create React App.

### In terminal
```
>> npm i create-react-app -g
>> npx create-react-app my-app
>> cd my-app
>> npm start
```
