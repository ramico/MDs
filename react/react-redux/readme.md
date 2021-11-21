# React-Redux

This is what need to be done to connect redux to a react application

## Packages to install

need to install *2 packages* `npm i redux react-redux` 

## Recommended folder structure

* **redux** *containing the whole thing* parallel to components

    * **store.js** *the store file*
    * **index.js** *a middleware passing action creators*
    * **rootReducer.js** *a container of combined reducers* **this approach adds a key to the selector**

    * **feathers{n}** *every feature resides in one aspect of the store*

        * **featureTypes** *action types (constants needed buy the reducer and the action creator)*
        * **featureActions** *action creators for the feature*
        * **featureReducer** *the reducer used to transmit actions to the store*

## Connecting to redux store

There are two ways to do so 

1. Using `connect()` : `import { connect } from 'react-redux'`

    This higher order function has two *optional parameters* arbitrarily: ***Note** selector is how to reach part of the store state*

    > pass the created component as a parameter to the returned function to connect it then export it  
    > **e.g** `export default connect(mapStateToProps, mapDispatchToProps)(CreatedComponent);`

    1. `mapStateToProps(state):obj` 

        ```js
        // Diffraction 
        const mapStateToProps = ({ mappedKey: /*selector*/ });
        ```

        > This function has an additional param {ownProps} you can do logic by passing them

    1. `mapDispatchToProps(dispatch):obj`

        ```js
        // Diffraction 
        const mapDispatchToProps = dispatch => ({ mappedKey: () => dispatch(/*call action creator*/) });
        ```

        > This function has an additional param {ownProps} you can do logic by passing them

1. Using hooks

    Both comes from *react-redux* package no mapping needed

    1. useSelector(state)

        ```js
        // Diffraction 
        const returnedRef = useSelector(state => /*selector*/);
        ```

    1. useDispatch

        ```js
        // Diffraction 
        const dispatch = useDispatch();
        // call it by dispatch(call action creator)
        ```

> you should wrap the components using the store with the react-redux component `Provider` passing the store prop for it 

## Redux devtools extension

* on the browser your using install extension *redux devtools*
* install package `npm i redux-devtools-extension -D` on your project
* import it in **store.js** `import { composeWithDevTools } from 'redux-devtools-extension';`
* when creating the store nest the applyMiddleware inside of `composeWithDevTools()` to debug your redux application in the browser

## logger and thunk middleware *same but different*

1. logger

only import 'createLogger' when you want to configure it otherwise just `import logger from 'redux-logger'` passing it to `applyMiddleware`
> make sure it's the **last** middleware in the list

1. thunk 

`.default` is used only for vanilla *javascript* no need to add it 