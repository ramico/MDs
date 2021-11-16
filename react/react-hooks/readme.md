# React Hooks 

Hooks are function used for functional components only and the don't you the `this` keyword

## REact.useState Hook

**Declaration** `const [ref, setRef] = useState(init)`

* if state is updated relating to a previous state set it via a callback
* keep in mind useState does not merge objects/Arrays use **...**

## React.useEffect Hook 

In useEffect you can mix and match regarding the needs lifecycle methods

lifecycle method | useEffects way
--- | ---
render | useEffect(()=>{})
componentDidMount | useEffect(()=>{},[]) *empty square brackets*
componentDidUpdate | useEffect(()=>{},\[dependency\])
componentWillUnmount | useEffect(()=>{*return ()=>{}*})

> ### dependency  
> A dependency is the variable by changing it's value affects the render  
> * it may be on other function calls **watch out**  
> * nest functions as Iffy inside the effect (easier)  
> * setting a state in prevState callback may be an option

## React.useContext 

uses the context API simplifying Consumer you wont be nesting consumer components instead

``` jsx
const myContextVar = useContext(myContextRef);
```

## React.useReducer

1. create the initial state and reducer function
2. use the hook

```jsx
const [state, dispatch] = useReducer(reducerFunction);
// dispatch(action)
```
## React.useCallBack *and* React.useMemo

both prototypes are the same *used for optimization* don't over do it 
*Only if it takes too much time*

> **fn(Function,\[dependencies\])**

* useCallback use it to memoize function reference
* useMemo use it to memoize the execution of a function

## React.useRef

> used for creating references from the virtual DOM  
> referencing difficult scoped variables

``` jsx
const ref = useRef();
// use ref.current
```
