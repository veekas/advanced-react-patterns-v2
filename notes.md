# Advanced React Patterns

## Toggle component

- you can destructure `currentState`... obviously, but pretty interesting

## Public class fields

- `this.handleClick` doesn't have `this` context, so
- you can make an arrow function, but that's not ergonomic, so
- you can bind function in constructor `this.handleClick = this.handleClick.bind(this)`, but that's also not great if there are many functions, so
- you can bind function as a class field `handleClick = function() {}.bind(this)`, but arrow functions are a thing, so
- you can just do lexical binding with arrow function `handleClick = () => {}`
- with this method, you don't have to have a constructor because state can be a simple class field `state = {}` and have all funcitons be lexically bound

## Compound components

- honestly blowing my mind right now...
- this would be great for UI libraries
- gives more rendering control to the user: same functionality but...
  - move visual parts of component into function components, add as `static` properties to `<Toggle />`
  - use `React.children.map` to give all children of `<Toggle />` the `on` state as a prop
- process
  - create static compound components (`On`, `Off`, `Button`) which access toggle state and click handler
  - receive those as props implicitly in the render method of toggle
  - so users can render however they like and state will be shared

## flexible compound components

- provides more flexible structure (e.g. nested div)
- process
  - `ContextComponent = React.createContext()`
  - in `render`, create `<ContextComponent.Provider value={propsToBeSent}>` and pass it children
  - in sub-components, wrap in `<ContextComponent.Consumer>` and run logic in there

## validate consumer

