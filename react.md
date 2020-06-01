# 1. Getting Started with React - An Overview and Walkthrough Tutorial
*walkthrough : 연습*<br><br>
written by **Tania Rascia** , **<https://www.taniarascia.com/getting-started-with-react/>**
> Thank you Tania Rascia!!

> I saw what looked like *a bunch of HTML mixed* with JavaScript and thought, isn't this what we've been trying to avoid? *What's the big deal with React?*

### Prerequisites
If you've never used JS or the DOM at all before, see below before trying to tackle React.
  1. Basic familiarity with HTML & CSS
  2. JS
  3. the DOM
  4. ES6 syntax and features
  5. Node.js and npm installed globally
  
### Goals

  1. Learn about essential React concepts! and related terms, such as Babel, Webpack, JSX, components, props, state, and lifecyle **(I think it is very important)**
  2. Build a very simple React app that demonstrates the above concepts.
  
  **Here's the source and a live demo of the end result.**<br>
      <https://github.com/taniarascia/react-tutorial><br>
      <https://taniarascia.github.io/react-tutorial/>
      
 ### WHAT IS REACT?
 
 1. JS library - one of the most popular ones(100,000 stars on Github)
 2. *React is not a framework* (unlike Angular)
 3. React is an open-source project created by **Facebook.**
 4. React is used to build user **interfaces(UI)** on the front end.
 5. React is the **view layer of an MVC application**
 
 One of the most important aspects of React is the fact that you can create **components** (what is a component??), which are like custom, **reusable HTML elements**, to quickly and efficiently build user interfaces. React also streamliness *(간소화하다)* how data is stored and handled, using **state and props** <br>
 
 We'll go over *(거듭 살피다)* all of this and more throughout the article, so let's get started!!
 
 ### Setup and Installation
 
 > There are a few ways to set up React, and I'll show you two so you get a good idea of how it works. <br>
 
 #### 1. Static HTML file
 1. not a popular way but it will be familiar and easy to understand if you've ever used a library like jQuery
 2. load in three CDNs in the `head` - React, React DOM, and Babel.
 3. finally we'll create a `script` tag where your custom code will live.
 
 **index.html**
 ```(.javascript)
 <!DOCTYPE html>
 <html>
     <head>
         <meta charset="utf-8" />
         <title> Hello React!!!</title>
         
         <script src="https://unpkg.com/react@^16/umd/react.production.min.js"></script>
         <script src="https://unpkg.com/react-dom@16.13.0/umd/react-dom.production.min.js"></script>
         <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
    
     </head>
     <body>
     
         <div id="root"></diiv>
         
         <script type="text/babel">
             // React code will go there
         </script>
     </body>
 </html>
 ```
 <br><br>
 
 ```
 class App extends React.Component {
     render() {
         return (
             <h1>Hello world!</h1>
         );
     }
 }
 
 ReactDOM.render(<App />, document.getElementById('root'))
 ```
 
 1. use ES6 classes to create a React component called `App`.
 2. add the `render()` method, *the only required method* in a class component, whice is used to render *DOM nodes* .
 3. Inside the `return`, Note that we're *not* returning a string here, so don't use quotes(따옴표 쓰기 ㄴㄴ!) around the element. **This is called** `JSX`
 4. Finally use the ReactDOM `render()` method to render the `App` class we created -> into `root`
 
 # 2. Create React App !!!!!!!!!!!!!!!!!!!!!!!!!!!!!
 The metohd I just used of loading JS libraries into a static HTML(as above) - is not very efficient, and is hard to maintain.
 > Fortunately, **Facebook has created** [Create React App][cra-link]
 
 [cra-link]: https://github.com/facebook/create-react-app "Go CRA LINK!"
 as environment that comes preconfigured with everything you need to build a React app. <br>
 It will create a live development server, use Webpack to automatically compile React, JSX, and ES6, auto-prefix CSS files, and use [ESLint][ESLink] to test and warn about mistakes in the code.
 
 [ESLink]: https://eslint.org/ "GO ESLint"

To set up `create-react-app`, run the following code in your terminal, one directory up from where you want the project to live.
```
npx create-react-app react-tutorial
```
Once that finished installing, move to the newly created directory and start the project.
```
cd react-tutorial
npm start
```
Once you run this command, a new window will popup at `localhost:3000` with your new React app.

>#### Create React App is very good for getting started for beginners as well as large-scale enterprise applications, but it's not perfect for every workflow. You can also create your own Webpack setup for React.

If you look into project structure, you'll see a `/public` and `/src` directory, along with the regular `node_modules`, `.gitignore`, `README.md`, and `package.json`

1. In `/public`, our important file is `index.html`, which is very similar to the static `index.html` file we made earlier - just a `root` div. This time, no libraries or scripts are being loaded in. The `/src` **directory will contain all our React code** <br>
To see how the environment automatically compiles and updates your React code, find the line that looks like this in /src/App.js.
```
To get started, edit [src/App.js] and save to reload.
```
And replace it with other text. Once you save the file, you'll notice `localhost:3000` compiles and refreshes with the new data.

**src/index.js**
```
import React from 'react'
import ReactDOMM from 'react-dom'
import './index.css'
```

**src/index.js**
creating our `App` component again.
```
class App extends Component {
    render() {
        return (
            <div className="App">
                <h1>Hello, react!</h1>
            </div>
        )
    }
}

ReactDOM.render(<App />, document.getElementById('root'))
```

If you back to `localhost:3000`, you'll see "Hello, react!" just like before. We have the beginnings of a React app now.

### React Developer Tools
#### There is an extension called 'React Developer Tools' that will make your life much easier when working with React! Download [React DevTools for Chrome][dev-link] , or whatever browser you prefer to work on.

[dev-link]: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi "Go link"

## Now we have all the tools and setup we need to actually begin working with React!!

### JSX: JavaScript + XML
- JS that looks like HTML in our React code, but it's not quite HTML.
- With JSX, we can create and use our own XML-like tags.

**JSX**
```
const heading = <h1 className="site-heading">Hello, React</h1>
```

- Using JSX is not mandatory for writing React.
- it's running `createElement` - and renders the same info(tag) 
**same output as the JSX above**

```
const heading = React.createElement('h1', {className: 'site-heading' }, 'Hello, React!')
```

- JSX is actually closer to JS **not HTML** 
    1. `className` is used instead of `class`
    2. Properties and methods in JSX are camelCase - `onClick` like JS
    3. **Self-closing** tags must end in a slash - e.g. <img **/>**
    4. JS expressions can also embedded inside JSX! using curly braces, including variables,
    functions, and properties
        ```
        const name = 'Tania'
        const heading = <h1>Hello,{name}</h1>
        ```
        -> {name} <<<<<< **here!!!**
    5.  JSX is easier to write and understand than creating and appending many elements in vanilla JS, and is one of the reasons people love React so much!!
    
### Components
- *so far : (제한된)어느 정도까지만*
- Almost everything in React consists of components, which can be class components or simple components
- We'll create **a new** file called `App.js` and put the component in there!!!!!!.
- It's really *WHAT I WANT!!**

- **src/index.js**
```
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import './index.css'

ReactDOM.render(<App />, document.getElementById('root'))
```

- **src/App.js**
```
import React, { Component } from 'react'

class App extends Compoenent {
    render() {
        return (
            <div className="App>
                <h1>Hello, React!</h1>
            </div>
        )
    }
}

export default App
```
- **We export the compoenent as `App` and load it in 'index.js'**

### Class Components
- Let's create another component. `Table.js` and fill it with the following data.
- **src/Table.js**
```
import React, { Component } from 'react'

class Table extends Component {
    render() {
        return (
            <table>
                <thread>
                    <tr>
                        <th>Name</th>
                        <th>Job</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Charlie</td>
                        <td>Janitor</td>
                    </tr>
                    <tr>
                        <td>Mac</td>
                        <td>Bouncer</td>
                    </tr>
                    <tr>
                        <td>Dee</td>
                        <td>Aspiring actress</td>
                    </tr>
                    <tr>
                        <td>Dennis</td>
                        <td>Bartender</td>
                    </tr>
                </tbody>
            </table>
        )
    }
}

export default Table
```
- **src/App.js**

```
import Table from './Table'
```

- **src/App.js**
```
import React, { Component } from 'react'
import Table from './Table'

class App extends Component {
    render() {
        return (
            <div className="container">
                <Table />
            </div>
        )
    }
}

export default App
```

### Simple Components
- function
-doesn't use the `class` keyword
- make two simple components for it - a table header, and a table body
- **src/Table.js**
```
const TableHeader = () => {
    return (
        <thead>
            <tr>
                <th>Name</th>
                <th>Job</th>
            </tr>
        </thead>
    )
}
```
- **src/Table.js**
```
const TableBody = () => {
    return (
        <tbody>
            <tr>
                <td>Charlie</td>
                <td>Janitor</td>
            </tr>
            <tr>
                <td>Mac</td>
                <td>Bouncer</td>
            </tr>
            <tr>
                <td>Dee</td>
                <td>Aspiring actress</td>
            </tr>
            <tr>
                <td>Dennis</td>
                <td>Bartender</td>
            </tr>
        </tbody>
    )
}
```

- **src/Table.js**

```
const TableHeader = () => { ... }
const TableBody = () => { ... }

class Table extends Component {
    render() {
        return (
            <table>
                <TableHeader />
                <TableBody />
            </table>
        )
    }
}
```
- **A class component must include `render()`, and the `return` can only return one parent element.**

### Props
- **One of the big deals about React is how it handles data, and it does so with properties, referred to as props, and with state. Now, we'll focus on handling data with props.**
- Let's move all that data to an array of objects, as if we were bringing in a JSON-based API.
```
class App extends Component {
    render() {
        const characters = [
            {
                name: 'Charlie',
                job: 'Janitor'
            },
            {
                name: 'Mac',
                job: 'Bouncer',
            },
            {
                name: 'Dee',
                job: 'Aspring actress',
            },
            {
                name: 'Dennis',
                job: 'Bartender',
            },
        ]
        
        return (
            <div className="container">
                <Table />
            </div>
        )
    }
}
```
- Now, we're going to pass the data **through to the child component** `Table` with properties, kind of how you might pass data through using `data-` attributes.
- We can call the property whatever we want, as long as it's not a reserved keyword, so I'll go with `characterData` !!
- **src / App.js**
```
return (
    <div className="container">
        <Table characterData={characters} />
    </div>
)
```
- Now that data is being passed through to `Table` - we have to work on accessing it from the other side.
- **src / Table.js**
```
class Table extends Component {
    render() {
        const { characterData } = this.props
        
        return (
            <table>
                <TableHeader />
                <TableBody characterData={characterData} />
            </table>
        )
    }
}
```
- If you open up React DevTools and inspect the `Table` component, you'll see the array of data in the property.
- The data that's stored here is known as the virtual DOM, which is a fast and efficient way of syncing data with the actual DOM.
- Props are an effective way to pass existing data to a React component, however the component cannot change the props - they're read-only.

### State
- With props, we have a one way data flow, but with state we can update private data from a component.
- You can think of state as any data that should be saved and modified without **necessarily being added to a database**
- adding and removing items from a shopping cart before confirming your purchase.

- To start, we're going to create a `state` object.
- **src / App.js**
```
class App extends Component {
    state = [
            {
                name: 'Charlie',
                job: 'Janitor'
            },
            {
                name: 'Mac',
                job: 'Bouncer',
            },
            {
                name: 'Dee',
                job: 'Aspring actress',
            },
            {
                name: 'Dennis',
                job: 'Bartender',
            },
        ]
}
```
- **You must use** `this.setState()` **to modify an array. Simply applying a new value to** 'this.state.property' **will not work.**
- **src / App.js**
```
removeCharacter = index =>{
    const { characters } = this.state
    
    this.setState({
        characters: characters.filter((character, i) =>{
            return i !== index
        }),
    }),
}
```
- **The `onClick` function must pass through a function that returns the `removeCharacter()` method, otherwise it will try to run automatically.**

### Submitting Form Data
- **Previously, it was necessary to include a `constructor()` on React class components, but it's not required anymore.**
- **src / Form.js**
```
import React, { Component } from 'react'

class Form extends Component {
    initialState = {
        name: '',
        job: '',
    }
    
    state = this.initialState
}
```

- **src / Form.js**
```
handleChange = event => {
    const { name, value } = event.target
    
    this.setState({
        [name]: value,
    })
}
```

### Pulling in API Data
- Lyfecycle is the order in which methods are called in React.
- Mounting refers to an item being inserted into the DOM.

### Building and Deploying a React App
- Now, if you just want to compile all the React code and place it in the root of a directory somewhere, all you need to do is run the following line
```
npm run build
```
