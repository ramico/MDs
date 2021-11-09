# React 

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