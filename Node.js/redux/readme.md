# Redux

Predictable state container for javascript apps.

## Redux units

### Action
is the way in with the **js** application interacts with the store

> The action is an object returned from a function called an **Action creator** declared in two conventions

* basic 

    ```js
    const ac_doSomething = (/*...*/) => ({type:'UPPER_SNAKE',data:/*...*/})
    ```
* flex *facebook way*

    ```js
    const ac_doSomething = (/*...*/) => ({type:'camelCase',payload:{/*...*/}})
    ```

### Reducer 

A pure function that stores how app state changes in the response to the action made by the client

> A reducer doest **merge objects**

e.g
```js
const reducer = (state = initialState,action) => {
    switch(action.type){
        case ACTION_ONE:
            return {...state, keyToUpdate: value};
        default:
            return state
    }
}
```

### Store

Is data is stored for the application use it by installing Redux `npm i redux` and importing in JS syntax `const redux = require('redux')`

#### Responsibilities

Responsibility | description
--- | ---
`redux.createStore(reducer)` | hold the stare
`store.getState()` | access to the state
`store.subscribe(()=>{}):unsubscribeFN` | event listener when state is updated
`state.dispatch(action)` | allow state to be updated
`unsubscribeFN()` | handling unregistering listeners 

## Combining reduces 

use the `store.combineReducers()` passing an object as follows *notice naming convinsions*

``` js
const rootReducer = store.combineReducers({
    key1: reducer1,
    key2: reducer2,
    /// choose good key names
});
```

## Middleware

Functionalities that build over the reducer; to use it add `store.applyMiddleware(Function)` as follows
> `const store = createStore(reducer,applyMiddleware(middlewareFN)) `

### logger middleware

1. install it `npm i redux-logger`
1. require it or import it
1. call it's createLogger function and store the returned value
1. add the value to the store 

``` js
const reduxLogger = require('redux-logger');
const logger = reduxLogger.createLogger();

const store = createStore(reducer,applyMiddleware(logger))
```

### Thunk middleware

#### installation 

`npm i redux-thunk`

#### usage 

> Thunk is higher order function returning a higher order function to implement async action 
*code parts as follows*

```js
//  some imports 
const thunk = require('redux-thunk').default

// action creator
const ac_fn = () => async dispatch => {/*say axios code dispatching many actions*/}

// finally in the store 
const store = createStore(reducer, applyMiddleware(thunk));
```





