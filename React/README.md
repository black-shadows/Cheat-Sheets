# 🌈 React Cheat Sheet

> A simple cheat sheet for facilitate the process in the workshops and event about React. Let me know if you see any problem, I'll love a pull request for improve this document.

## Table of contents

- [x] [Installation](#installation)
- [x] [No configuration](#no-configuration)
- [x] [ReactDOM](#reactdom)
- [x] [Functional Stateless Component](#functional-stateless-component)
- [x] [Class Component](#class-component)
- [x] [Composition](#composition)
- [x] [Module component](#module-component)
- [x] [Hot Module Replacement](#hot-module-replacement)
- [x] [Props](#props)
- [x] [State](#state)
- [x] [Methods and Events](#methods-and-events)
- [x] [State manipulation](#state-manipulation)
- [x] [Bindings](#bindings)
- [ ] [Refs](#refs)
- [ ] [Keys](#keys)
- [ ] [Component Lifecycle](#component-lifecycle)
- [ ] [Inline Styles](#inline-styles)
- [ ] [React Router](#react-router)
- [ ] [Storybook](#storybook)
- [ ] [Tests](#tests)
- [ ] [a11y](#a11y)
- [ ] [API comunication](#api-comunication)
- [ ] [Flux](#flux)
- [ ] [Redux](#redux)
- [ ] [MobX](#mobx)
- [ ] [Best Practices](#best-practices)
- [ ] [Concepts](Concepts)
    - [ ] [Immutable](#immutable)
    - [ ] [Functionnal programing](#functionnal-programing)
    - [ ] [Virtual Dom](#virtual-dom)
- [x] [ES6](#es6)
    - [x] [Arrow Functions](#arrow-functions)
        - [x] [Syntax](#syntax)
        - [x] [Advanced Syntax](#advanced-syntax)
    - [x] [Spread Operations](#spread-operations)
        - [x] [Spread in array literals](#spread-in-array-literals)
        - [x] [Spread in object literals](#spread-in-object-literals)

---

## Installation

* Add the tags in your HTML
    ```HTML
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    ```
* Run this scripts in your terminal
    ```SSH
    $ npm install react react-dom
    ```
 
 **[⬆ back to top](#table-of-contents)**
---
 
## No configuration

Just start with React no configuration (run the scripts bellow in your terminal)
* Install the React
    ```SSH
    $ npm install -g create-react-app
    ```
* Create your application (change `myApp` to your application name)
    ```
    $ create-react-app myApp
    ```
* Go to the application folder and install the dependencies
    ```
    $ cd myApp
    $ npm install
    ```
* Start your application
    ```
    $ npm start
    ```
* Go to the browser by `URL` bellow and see your beautiful application   
    - [localhost:8080](http://localhost:8080)

**[⬆ back to top](#table-of-contents)** 
---

## ReactDOM

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render( <h1>Hello React Ladies</h1>, document.getElementById('root') );
```

**[⬆ back to top](#table-of-contents)**
---

## Functional Stateless Component

```JS
import React from 'react';

const Button = () =>
    <button> Apply</button>

export default Button;
```

```JS
import React from 'react';

const Button = ({ onClick, className = 'button', children  }) =>
    <button
        onClick={ onClick }
        className={ className }
        type='button'
    >
        { children }
    </button>

export default Button;
```

**[⬆ back to top](#table-of-contents)**
---

## Class Component

```JS
import React, { Component } from 'react';

class MyComponent extends Component {
    render() {
        return (
            <div className="main">
                <h1>Helo Devas</h1>
            </div>
        );
    }
}

export default MyComponent;
```

```JS
import React, { Component } from 'react';

class MyComponent () extends Compnent {
    constructor ( props ) {
    super(props);
    this.state = { message: 'Helo Devas' }
    };

    render() {
        return (
            <div className="main">
                <h1>{ this.state.message }</h1>
            </div>
        );
    }
}

export default MyComponent;

```

**[⬆ back to top](#table-of-contents)**
--- 

## Composition

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class Love extends Component {
    render() {
        return (
            <div clssName="love">
                <h1>My love</h1>
            </div>
        );
    }
}

class LoveList extends Component {
    render() {
        return (
            <div>
                <Love />
                <Love />
                <Love />
                <Love />
            </>
        );
    }
}

ReactDOM.render(
    <Love />,
    document.getElementById(´root´)
);

**[⬆ back to top](#table-of-contents)**
```

## Module component

```JS
//App.js
import React, { Component } from 'react';

class App extends Component {
    render() {
        return (
            <div className="app">
                <p>My App</p>
            </div>
        );
    }
}

export default App
```

```JS
//Index.js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import App from './App.js';

class Index extends Component {
    render() {
        return (
            <div className="app">
                <App />
            </div>
        );
    }
}


ReactDOM.render (
    <Index />,
    document.getElementById('root')
);

```

**[⬆ back to top](#table-of-contents)**
---

## Hot Module Replacement
* Retain application state which is lost during a full reload.
* Save valuable development time by only updating what's changed.
* Tweak styling faster -- almost comparable to changing styles in the browser's debugger.

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import MyComponent from './MyComponent';

ReactDOM.render( <MyComponent />, document.getElementById('root') );

if (module.hot) {
    module.hot.accept();
}
```

**[⬆ back to top](#table-of-contents)**
---

## Props

```JS
import React, { Component } from 'react';

class App extends Component {
    render() {
        return (
            <div className="app">
                <p>My App {this.props.name}</p>
            </div>
        );
    }
}

class Index extends Component {
    render() {
        return (
            <div className="app">
                <App name="Simone"/>
            </div>
        );
    }
}

export default Index;
```

**[⬆ back to top](#table-of-contents)**
---

## State

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor(props) {
        super(props);
        this.state = {messages: 0};
    } 

    render() {
        return (
            <div className="app">
                <p>My messages: {this.state.messages}</p>
            </div>
        );
    }
}

export default App;
```

**[⬆ back to top](#table-of-contents)**
---

## Methods and Events

```JS
import React, { Component } from 'react';

class App extends Component {

    escreve() {
      console.log("Eu te amo");
    }

    render() {
        return (
            <div className="app">
                <button onClick={this.escreve}>save</button>
            </div>
        );
    }
}

export default App;
```

**[⬆ back to top](#table-of-contents)**
---

## State manipulation

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor() {
        super();
        this.state = { like: 0 };
    } 

    isLiked = () => {
      this.setState({ like: this.state.like + 1});
    }

    render() {
        return (
            <div className="app">
                <button onClick={ this.isLiked }>{ this.state.like }</button>
            </div>
        );
    }
}

export default App;
```

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor() {
        super();
        this.state = { messages: ['JS', 'React'] };
    } 

    addMessages = () => {
        const updateMessages = [...this.state.messages, 'Polymer']
        this.setState({ messages: [...updateMessages] })
    }

    render() {
        return (
            <div className="app">
                <button onClick={this.addMessages}>add</button>
                {console.log(this.state.messages) /* ['JS', 'React', 'Polymer'] */}
            </div>
        );
    }
}

export default App;
```


**[⬆ back to top](#table-of-contents)**
---
d
## Bindings

```JS
import React, { Component } from 'react';

class MyComponent extends Component {
    constructor () {
    super();

    this.state = { list: list };

    this.doSomethingElse = this.doSomethingElse.bind(this);
    };

    doSomething = () => {
        // do something
        /* if don't have a parameter, you can use arrow function
           and don't need to use bind */
    }

    doSomethingElse ( itemId ) {
        // do something else
    }

    render() {
        return (
            <div className="main">
                {this.state.list.map( item =>
                ...
                    <button 
                        onClick={ this.doSomething } 
                        type="button"
                    >
                        Some Thing
                    </button>

                    <button 
                        onClick={ () => this.doSomethingElse( item.objectID ) } 
                        type="button"
                    >
                        Some Thing Else
                    </button>
                ...
                )}
            </div>
        );
    }
}

export default MyComponent;
```

---

# ES6

## Arrow Functions

### Syntax

  #### Basic syntax
    ```JS
    ( param1, param2, ..., paramN ) => { statements }

    ( param1, param2, ..., paramN ) =>  expression

    ( singleParam ) => { statements }

    singleParam => { statements }

    () => { statements }
    ```
  #### Advanced Syntax
    ```JS
    params => ({ foo: bar }) /* return an object literal expression */

    ( param1, param2, ...ladies ) =>  { statements } /* rest parameters */

    ( language = JS, ladies, ..., framework = React ) => { statements } /* default parameters */

    const sum = ( [num1, num2] = [1, 2], { x: num3 } = { x : num1 + num2 } ) => num1 + num2 + num3  /*  destructuring within the parameter list */
    sum() /* 6 */
    ```

---

## Spread Operations

### Spread in array literals
```JS
const basics = [ 'JS', 'HTML', 'CSS' ];
const frameworks = [ 'React', 'Vue' ];
const web = [ ...basics, ...frameworks ]; 
console.log(web); /* ['JS', 'HTML', 'CSS', 'React', 'Vue'] */

const addWeb = [ ...web, 'al11' ];
console.log(addWeb); /* ['JS', 'HTML', 'CSS', 'React', 'Vue', 'al11'] */
```

### Spread in object literals
```JS
const basics = { behavior: 'JS', markup: 'HTML' };
const style = 'CSS';
const web = { ...basics, style }; 
console.log(web); /* { behavior: "JS", markup: "HTML", style: "CSS" } */

const devFront = { framework: 'react', event: 'React Conf' };
const devBack = { framework: 'django', state: 'cool' };

const cloneDev = { ...devFront };
console.log(cloneDev); /* { framework: 'react', event: 'React Conf' } */

const merged = { ...devFront, ...devBack };
console.log(cloneDev); /* { framework: 'django', event: 'React Conf', state: 'cool' } */
```