# React

## Libs for small projects

``` html
<head>
    <script crossorigin src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
    <!-- in browser babel support -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<body>
    <!-- ... -->
    <script type="text/babel">
        // ...
    </script>
</body>
```

## Installation 2 methods

* Using **npx** recommended

1. `npx create-react-app my-app` app name should be in lowercase
1. Make my-app the current directory `cd my-app`
1. `npm start`

* Using **npm**

1. `npm -g create-react-app` install this package globally
1. `create-react-app my-app` app name should be in lowercase`
1. Make my-app the current directory `cd my-app`
1. `npm start`

## components 

### Creating and exporting
> #### Creating  
> To create a component you need to `import React from 'react'`  
> components and their must use PascalCasing
> #### Exporting  
> * Named exports: which enforces using same export reference wrapping the imported reference with curly braces  
> * Default export which allows us to pick whatever reference we choose

### Component types 

> #### A way to create components  
> `React.createElement(elem, attrib,ChildNode)`  
> Param | desc  
> :-: | ---  
> elem:string | The html element  
> attrib:obj | An object for DHTML attributes  
> childNode:HTML | children which may nest many calls


* Functional *a function that returns a component **one root***

    ``` jsx
    const Component = () => <h1>Hello world</h1>
    ```

* Class components 

    > **important note**  
    > it should extend the `React.Component`  
    > also override it's *render* function that returns the component  
    > ### Declaration  
    > ``` jsx  
    >  // use rce react snippet om vscode
    > class Component extends React.Component {  
    > render = () => <h1>Hello world!</h1>;
    > }  
    > ```

**this** keyword used for class components unused for functional components

## props and states

- | props | states
--- | --- | ---
Declared | Are passed to the component | are manages in the component
Changeability | read-only | can be changes in component body
functional access | props | useState
Class access | this.props | this.state

> ### The setState function of the class component  
> `this.setState(obj|Fn,callback)`  
> * first parameter can be an object resting the state *indirectly* or a function  
> * callback in short .then()  
> #### First function param  
> can have two parameters and it returns an object  
> param | desc  
> --- | ---  
> prev | previous state object  
> props | access the props object

## Events

Class components need to bind `this` keyword and there are *four* ways for that

1. Binding in render {performance not cool}

    ``` jsx
    render(){
        return <button onClick={this.fn.bind(this)}></button>;
    }
    ```

1. Binding in render with arrow function

    ``` jsx
    render(){
        return <button onClick={() => this.fn()}></button>;
    }
    ```

1. Binding in the class constructor {recommended by React}

    ``` jsx
    constructor() {
        this.fn = this.fn.bind(this);
    }

    render(){
        return <button onClick={this.fn}></button>;
    }
    ```
    
1.  Class property as an arrow function {recommended by React}

    ``` jsx
    fn = () => {
        // do something
    }
    render() {
        return <button onClick={this.fn}></button>;
    }
    ```
