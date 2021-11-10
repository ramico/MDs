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

* Using **npm** recommended 

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

> ### life-cycle stages class components  
> * Mounted: when the component is mounter to the dom  
> * Updated: when the component gets rerendered  
> * Unmounted: when the components gets removed from the dom  
> * Error handling: which may occur in  
>   * Duding mounting  
>   * from the life-cycle  
>   * from the constructor  
>   * from it's children

## props and states

\- | props | states
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

> #### props.children  
> the variable is always declared reads the **JSX** child nodes  
> if used and components has no children React discards it

## Events

Class components need to bind `this` keyword and there are *four* ways for that

1. Binding in render {performance not cool}

    ``` jsx
    render(){
        return <button onClick={this.fn.bind(this)}></button>;
    }
    ```

1. Binding in render with arrow function {easiest way to pass parameters}

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

## Conditional rendering

can be done in four ways 

1. **if/else keywords** you cant have a branching structure within **JSX** code

    ``` jsx
    render(){
        if(true){
            return <>something</>
        } else {
            return <>something else</>
        }
    }
    ```

1. **Elem var** stores the result of the branching structure

    ``` jsx
    render(){
        let res; 
        if(true){
            res = <>something</>;
        } else {
            res = <>something else</>;
        }
        return res;
    }
    ```

1. **?:** turnery operator cn be used within JSX components

    ``` jsx
    render(){
        return true ? <>something</> : <>something else</>;
    }
    ```

1. **&&** short circuit : ise it if you have {if A} case and don't have a B

    ```jsx
    render(){
        true && <>something</>;
    }
    ```

## Rendering list of items

When using loops to render children be aware of adding a unique key *React property which is not accessed* and it uses it to keep track for added elements.

`aList.map((e,i)=><li key={i}>{e}</li>)`

> ### **Important note**  
> Never use index as a key unless these conditions are met  
> * List does not have a unique id/field etc...  
> * List is never modified, sorted or filtered

## Styling 

styling can be applied to React in three ways

1. *CSS* files

    > By creating a typical css file good selector configuration is required  
    > to use it just `import './file.css'`  

1. inline styling 

    > React allows assigning an object to the style attribute for html components  
    > the object properties must be camelCased *DHTML*

1. Module allows for making css classes properties to an object via the following

    1. create a file *style.module.css* with some classes as needed
    1. import it `import style from 'style.module.css'`
    1. set the JSX attribute for a component `<p className={style.aClass}>`

    > **Note** this method reduces css conflicts

## Forms

* Values should be connected to the component state
* to pick up values from input/textarea or a select handle the onChange event
* use the `e` param in the event handler to pick up the value `e.target.value`

> **Note** you can use either a submit button or onSubmit for event to handle the submission  
> `e.preventDefault()` prevents the form from it default submission behavior of refreshing the page



