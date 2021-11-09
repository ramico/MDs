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

## Installation 

1. `npx create-react-app my-app` app name should be in lowercase
1. Make my-app the current directory `cd my-app`
1. `npm start`

## Components

> **Important**  
> Component name must begin with a capital letter

### Displaying component 

`ReactDom.render(aComponent,document.querySelector('#element'))`

### Component types 

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
    > class Component extends React.Component {  
    > render = () => <h1>Hello world!</h1>;
    > }  
    > ```

## Component properties

> **Important note**  
> props are read-only, meaning components cannot modify their props. 

* Functional components

    > Props is an object added as the argument  
    > accessed via `const el = <Component prop="state"/>`

* Class components

    ``` jsx
    class Component extends React.Component {
        render = () => <h1>Hello, {this.props.name}</h1>;
    }
    ```

## States in comparison with props 

state | props
--- | ---
Manage component data  | passes data to components
Can modified via `setState()` | Are read-only *cannot be modified*

> The `setState()` method results in re-rendering the component affected.  
> `import {useState} from 'react'` usage `const [var,setVar()] = useState(initVal)`

## Shared states

A parent can share states and props *downwards* only via props

## Life-cycle

> ### Definitions    
> * **Mounting**: is the process when a component is rendered on the page.  
> * **Unmounting**: is the process when a component is removed from the page.  
> ### Methods  
> * `componentDidMount()`: method is called when a component is rendered on the page.  
> * `componentDidUpdate()`: method is called when a component is updated in the DOM.  
> * `componentWillUnmount()`: is invoked immediately before a component is unmounted and destroyed.

### Usage 

functional components use *useEffects* a hook imported `import {useEffects} from 'react'` 

class component | functional component
:-:|:--
`componentDidUpdate()` | useEffects(():void=>{})
`componentWillUnmount()` | useEffects(():cleanup=>{})
`componentDidMount()` |  useEffects()((()=>{},\[dependencies\])=>{})

### Redux

> #### Installation  
> is installed via `npm i redux react-redux` *2 packages*  
> #### Deploying steps  
> 1. instantiate the state  
> 1. *Create the action* => {type:'NAME',data:any} **Name should be written *upper(SNAKE_CASE)***   
> 1. *create a reducer* function to branch `action.type` for different updates  
> 1. *create the store* `const store = createStore(reducer)`
> 1. *Create the component* that is going to use the state as it was declared and sent via **props**  
> 1. *Create `mapStateTOProps(state)`* function that returns the required stuff   
> 1. *Create the mapDispatchToPropsObject* that is going to hold the related functions respectively  
> 1. *Call the `connect(mapStateToProps?,mapDispatchToPropsObject?):InferableComponentEnhancerWithProps`* and call the returned value passing the *created component*  
> 1. finally render the ConnectedComponent wrapped im `<Provider store={store}>`  
> ### Notes and imports  
> ``` js  
> import { connect, Provider } from 'react-redux'; 
> import { createStore } from 'redux';  
> // connect small c; upper C would be an interface  
> ```  
> *Rest of the methods are customizable to your taste*  
> ### useSelector sand useDispatch  
> equivalent to `mspStateToProps()`,`mapDispatchToProps()`  respectively
>  
> ``` jsx  
> import {useSelector, useDispatch} from 'react-redux'  
> // import your action 
> const Component = () => {  
>   const dispatch = useDispatch();
>   const contacts = (state) => state.contacts;  
>   return (  
>       <>  
>           <p>{contacts.join(', ')}<p>  
>           <button onClick={dispatch(/*call your action*/)}>  
>           </button>  
>       </>  
>   );  } // End function  
> ```  
> ![SOLO certificate](https://user-images.githubusercontent.com/5300122/140267918-8b3a04be-dfdb-4424-8fef-88e9fed7e68f.jpg)