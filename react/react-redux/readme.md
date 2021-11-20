# React-Redux

This is what need to be done to connect redux to a react application

## Packages to install

need to install *2 packages* `npm i redux react-redux` 

## Recommended folder structure

* **redux** *containing the whole thing*

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

    1. `mapDispatchToProps(dispatch):obj`

        ```js
        // Diffraction 
        const mapDispatchToProps = dispatch => ({ mappedKey: () => dispatch(/*call action creator*/) });
        ```
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
