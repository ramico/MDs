# React

## Libs for small projects

```html
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

- Using **npx** recommended

1. `npx create-react-app my-app` app name should be in shish-kebab-casing
1. Make my-app the current directory `cd my-app`
1. `npm run start`

- Using **npm**

1. `npm -g create-react-app` install this package globally
1. `create-react-app my-app` app name should be in lowercase`
1. Make my-app the current directory `cd my-app`
1. `npm run start`

## Components

### Creating and exporting

> #### Creating
>
> To create a component you need to `import React from 'react'` for react version < 17  
> components must use PascalCasing
>
> #### Exporting
>
> - Named exports: which enforces using the same export reference wrapping the imported reference with curly braces
> - Default export which allows us to pick whatever reference we choose

### Component types

> #### A way to create components
>
> `React.createElement(elem, attrib,ChildNode)`  
> Param | desc  
> :-: | ---  
> elem:string | The html element  
> attrib:obj | An object for DHTML attributes  
> childNode:HTML | children which may nest many calls

- Functional \*a function that returns a component **one root**

  ```jsx
  const Component = () => <h1>Hello world!</h1>;
  ```

- Class components

  > **Important note**  
  > it should extend the `React.Component`  
  > also override it's _render_ function that returns the component
  >
  > ### Declaration
  >
  > ```jsx
  > // Use rcc react snippet om vscode
  > class Component extends React.Component {
  >   render = () => <h1>Hello world!</h1>;
  > }
  > ```

**this** keyword used for class components only

## life-cycle stages class components

> - Mounted: when the component is mounted to the DOM
> - Updated: when the component gets rerendered
> - Unmounted: when the components gets removed from the DOM
> - Error handling: which may occur in
>   - During mounting
>   - from the life-cycle
>   - from the constructor
>   - from it's children

### Mounting methods

1. `constructor` : which will get called whenever a component is created
<dl style="margin-left:25px">
<dt> Do </dt>
<dd style="margin-left:10px;">Initialize state with super(props) and bindEvent handlers</dd>
<dt> Don't </dt>
<dd style="margin-left:10px;">Cause side effect e.g HTTP request</dd>
</dl>
1. <code> **static** getDerivedStateFromProps(state, props)</code>:&nbsp;When the state of the component relies on _props_
<dl style="margin-left:25px">
<dt> Don't </dt>
<dd style="margin-left:10px;">Cause side effect e.g HTTP request</dd>
<dt> Why static </dt>
<dd style="margin-left:20px">To discourage any side-effects during the render phase</dd>
</dl>
1. `render()` : The only **required** method, children components lifecycle methods are also executed
<dl style="margin-left:25px">
<dt> Don't </dt>
<dd style="margin-left:10px;">Cause side effect, interact with the DOM <b>OR</b> make ajax calls</dd>
</dl>
1. `componentDidMount()` : Invoked immediately after the component and all it's children have rendered
<dl style="margin-left:25px">
<dt>Do</dt>
<dd style="margin-left:10px;">Cause side effect, interact with the DOM <b>OR</b> make ajax calls</dd>
</dl>

### Updating methods

1. <code>constructor()</code>:&nbsp;Every time the component is <em>rerendered</em>

1. <code>**static** getDerivedStateFromProps(state, props)</code>:&nbsp;Every time the component is <em>rerendered</em>
<dl>
<dt>Do</dt>
<dd style="margin-left:10px;">Set the state</dd>
<dt>Don't</dt>
<dd style="margin-left:10px;">Cause side effect, interact with the DOM <b>OR</b> make AJAX calls</dd>
</dl>

1. <code>shouldComponentUpdate(nextProps,nextState):boolean</code>:&nbsp; A performance optimization method detecting wither or not the component should be <em>Rerendered</em>
<dl style="margin-left:25px">
<dt>Don't</dt>
<dd style="margin-left:10px;">Cause side effect, interact with the DOM <b>OR</b> make AJAX calls</dd>
</dl>

1. <code>render()</code>:&nbsp;same as before

1. <code>getSnapshotBeforeUpdate(nextProps,nextState)?:any</code>:&nbsp; Called right before changer are reflected from the virtual DOM to the DOM
<dl style="margin-left:25px">
<dt>Do</dt>
<dd style="margin-left:10px;">Get some info from the Dom</dd>
<dt>Note</dt>
<dd style="margin-left:10px">this method returns null or a value passed as a third parameter to the next function</dd>
</dl>

1. <code>componentDidUpdate(prevProp, prevState, snapshot?)</code>:&nbsp; Called after rendering took place
<dl style="margin-left:25px">
<dt>Do</dt>
<dd style="margin-left:10px;">Cause side effect, interact with the DOM <b>OR</b> make AJAX calls</dd>
</dl>

### Unmounting method

- <code>componentWillUnmount()</code>&nbsp;method is invoked immediately before component is destructed
    <dl style="margin-left:25px">
    <dt>Do</dt>
    <dd style="margin-left:10px;">clean up free resources</dd>
    <dt>Don't</dt>
    <dd style="margin-left:10px;">use <code>setState</code></dd>
    </dl>


### Error handling

1. <code>**static** getDerivedStateFromError(errorObject,info)</code>
<dl style="margin-left:25px">
<dt>Do</dt>
<dd style="margin-left:10px;">return the state object with a boolean property set to <em>true</em></dd>
</dl>

1. <code>componentDidCatch()</code>&nbsp; this method returns redundant details
<dt>Don't</dt>
<dd style="margin-left:10px;"><strong>don't</strong> use this method unless you need the already <em>outputted</em> error</dd>
</dl>

## props and states

| \-                | props                       | states                           |
| ----------------- | --------------------------- | -------------------------------- |
| Declared          | Are passed to the component | are managed in the component     |
| Changeability     | read-only                   | can be changes in component body |
| functional access | props                       | useState                         |
| Class access      | this.props                  | this.state                       |

> ### The setState function of the class component
>
> `this.setState(obj|Fn,callback)`
>
> - first parameter can be an object resting the state _indirectly_ or a function
> - callback in short .then()

> #### First function param
>
> can have two parameters and it returns an object  
> param | desc  
> --- | ---  
> prev | previous state object  
> props | access the props object

> #### props.children
>
> the variable is always declared reads the **JSX** child nodes  
> if used and component has no children _React discards it_

## Events

Class components need to bind `this` keyword; there are _four_ ways for that

1. Binding in render {performance not cool}

   ```jsx
   render(){
       return <button onClick={this.fn.bind(this)}></button>;
   }
   ```

1. Binding in render with arrow function {easiest way to pass parameters}

   ```jsx
   render(){
       return <button onClick={() => this.fn()}></button>;
   }
   ```

1. Binding in the class constructor {recommended by React}

   ```jsx
   constructor() {
       this.fn = this.fn.bind(this);
   }

   render(){
       return <button onClick={this.fn}></button>;
   }
   ```

1. Class property as an arrow function

   ```jsx
   fn = () => {
       // do something
   }
   render() {
       return <button onClick={this.fn}></button>;
   }
   ```

## Conditional rendering

can be done in four ways

1. **if/else keywords** you can't have a branching structure within **JSX** code

   ```jsx
   render() {
       if(true){
           return <>something</>;
       } else {
           return <>something else</>;
       }
   }
   ```

1. **Element variables** stores the result of a branching structure

   ```jsx
   render() {
       let res;
       if(true){
           res = <>something</>;
       } else {
           res = <>something else</>;
       }
       return res;
   }
   ```

1. **?:** turnery operator can be used within JSX components

   ```jsx
   render() {
       return true ? <>something</> : <>something else</>;
   }
   ```

1. **&&** short circuit: Use it if you have {if A} case and don't have a B

   ```jsx
   render(){
       true && <>something</>;
   }
   ```

## Rendering list of items

When using loops to render children be aware of adding a unique key _React property which is not accessed_ and it uses it to keep track for added elements.

`aList.map((e,i)=><li key={i}>{e}</li>)`

> ### **Important note**
>
> Never use index as a key unless these conditions are met
>
> - List does not have a unique id/field etc...
> - List is never modified, sorted or filtered

## Styling

Styling can be applied to React in three ways

1. _CSS_ files

   > By creating a typical css file good selector configuration is required  
   > to use it just `import './file.css'`

1. Inline styling

   > React allows assigning an object to the style attribute for html components  
   > the object properties must be camelCased _DHTML_

1. Module allows for making css classes properties to an object via the following

   1. create a file _style.module.css_ with some classes as needed
   1. import it `import style from 'style.module.css'`
   1. set the JSX attribute for a component `<p className={style.aClass}>`

   > **Note** this method reduces CSS conflicts

## Forms

- Values should be connected to the component state
- To pick up values from input/textarea or a select handle the onChange event
- Use the `e` param in the event handler to pick up the value `e.target.value`

> **Note** you can use either a submit button or onSubmit for event to handle the submission  
> `e.preventDefault()` prevents the form from it's default submission behavior of refreshing the page

## PureComponent `React.PureComponent`

A component that is rendered once you should make sure that neither it nor it's children gets rerendered _better to be memoized_

## memo `React.memo`

A function that memoizes a component from unnecessary renders

## `React.Fragment` the null component

since react components should Have one root component you may either wrap the return with `<></>` **OR** React.Fragment tags the last one may use a key attribute

## React references

A way to make React select items from the dom

> ### implementations
>
> - <code> this.ref = React.createRef(); </code>
> - <code> this.ref = (elem=>this.ref=elem)(); </code>

### Usage

Add the ref attribute to the intended component/element then access it via `this.ref.current`

### Forwarding references

A way to pass references to child components by just adding the component declaration function as a parameter to the `React.forward()`function **remember** to pass reference to the functional component via second parameter

## `ReactDom.createPortal()`

A way to pass component(s) to an element out of **React root element** use the method as `ReactDom.render`

## sharing functionality patterns

1. render props

   ### Steps

   1. Create a parent component that will pass functionality to inherit
   1. the parent should call a props function conventionally `render`
   1. implement the parent component in the virtual DOM passing function definition

      ```jsx
      <parent>{(a, b) => <Child a={a} b={b} /> /*children can be passed as a function as well*/}</parent>
      ```

   1. call the sent prop function in the Parent Definition file while rendering

      ```jsx
      <>{this.props.render(a, b)}</>
      ```

1. HOC _higher order component_

   > **Definition** A pattern that takes a component as an argument returning an enhanced version of it and acts as a Parent Class

   ### Requirements

   - A functional component to be exported having a component as an argument
   - An inner component adding normal functionality sending them via attributes
   - using this functional component as a function

   ### Naming conventions

   - the HOC name starts using `With.....`
   - As normal component PascalCasing must be used
   - The argument of the outer function called `WrappedComponent`
   - The inner component must have the same name

   > NOTES:
   >
   > - in the inner component addons are passed via attributes and received via props
   > - if `WrappedComponent` may receive props from outside add `{...this.props}` oe you wont be able to receive them
   > - finally if you want to pass data from the `WrappedComponent` just add another argument

   ### Example

   ```jsx
   //HOC file
   import React, { Component } from 'react';

   const WithCounter = (WrappedComponent, increase) => {
   class WithCounter extends Component {
       constructor(props) {
       super(props);

       this.state = {
           count: 0,
       };
       this.incrementCount = this.incrementCount.bind(this);
       }
       incrementCount() {
       this.setState(prev => ({ count: prev.count + increase }));
       }
       render() {
       return (
           <WrappedComponent
           count={this.state.count}
           incrementCount={this.incrementCount}
           {...this.props}
           />
       );
       }
   }
   return WithCounter;
   };

   export default WithCounter;

   // child snippiest
   export default WithCounter(HoverCounter, 5);
   ```

1. Context

- A context can be passed down in the virtual DOM skipping some levels
- to create a context `const ref = React.createContext(init)`
- a context has two important properties **Provider** & **consumer**

  > **provider** is a component may be used either with selected const name or `<contextref.provider>`  
  > **consumer** on the other hand is where the value is deployed selected const name or `<contextref.consumer>`

- the provider passes the value prop and the consumer defines a function in it's tag with the value as an argument

> ### class components
>
> you may either write below class definition `classref.contextType = context` or in the class write `static contextType = contextRef`  
> render the context in this case using `this.context`  
> **flows of the static approach**
>
> 1. only works in class components
> 1. single context

> **final note** init is used when no provider exists in the upper root of the virtual DOM
