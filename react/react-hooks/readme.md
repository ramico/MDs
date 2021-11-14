# React Hooks 

hooks are for functional components only and the don't you the `this` keyword

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



