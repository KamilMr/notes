# React

## Hooks

### useEffect
- It is mechanism that helps synchronise side effect with state of you component.
- The Effect Hook lets you perform side effects in function components.
- Hooks embrace JavaScript closures - `useEffect` has access to scope of component.
- Side effects: Data fetching, setting up a subscription, and manually changing the DOM.
- You can think of `useEffect` Hook as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.
- It might be easier to think that effects happen “after render”.
- There are two common kinds of side effects in React components: those that don’t require cleanup.
- You can pass two arguments, first is required.
    a) `() => {}`
    b) dependency array: `no arr, [], [these, states]`
- It runs after React finishes rendering the component and React guarantees the DOM has been updated by the time it runs the effects.
- When you add `useEffect(() => {}, [])` you say React to run function inside `useEffect` when component is mounted
- Every time we re-render, we schedule a different effect, replacing the previous one, each effect “belongs” to a particular render.
-
