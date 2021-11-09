# React Render

When and how React chooses to render components

> **Note**: If strict mode enabled render happen twice in development mode

## one JSX element with a scalar value

<dl>
    <dt>old state == new state</dt>
    <dd> the element does not rerender </dd>
    <dt>old state != new state</dt>
    <dd> the element does rerender and is the state matched the old state it'll rerender one more time</dd>
</dl>

## one JSX element with a multi value

> **Important note**  
> Directly mutating the state is a way to cause bugs

<dl>
    <dt>Mutable changes</dt>
    <dd> the element does not rerender </dd>
    <dt>Immutable changes </dt>
    <dd> the element does rerender </dd>
</dl>

## more than one JSX element *parent and child*

<dl>
    <dt>old state == new state</dt>
    <dd> the element and it's children wont rerender </dd>
    <dt>old state != new state</dt>
    <dd> the element and the children will rerender once </dd>
</dl>

> if parent state did not change after a change only the parent will rerender

### Optimizing parent child rerendering

> `React.memo(child)` This function Memoizes the shallow state of the child component 

isOk | Using same element reference technique | Using `React.memo(child)`
--- | --- | ---
if | parent state changes |  state change does rerender the child unnecessarily
not if | changes were in it's props | component is complicated, not hte final node, impure or props passes object reference (JSON,Array,Function))

> **Impure component**: are those that their output changes with something other than their props/state

> #### A fix for memoizing objects and functions  
> **For objects** use `React.useMemo` hook  
> **For functions** use `React.useCallback` hook

## Context {An expensive approach in react *not the best*}

If the tree is somewhat long

* memoize the immediate child of the parent that sends the context and wrap the memoized component in the context provider
* Or use children prop.