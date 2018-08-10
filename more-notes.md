# combine this with notes on other machine

## compound components: validation

```js
function ToggleConsumer(props) {
  return (
    <ToggleContext.Consumer {...props}>
      {context => {
        if (!context) {
          throw new Error(
            `Toggle compound components cannot be
            rendered outside the Toggle component`,
          )
        }
        return props.children(context)
      }}
    </ToggleContext.Consumer>
  )
}
```

## compound components: prevent rerenders

- by adding the `this.toggle` to state, and changing the Provider value prop to `value={this.state}`, it prevent unnecessary rerenders in larger applications

## render props

- if function is not using instance props or methods (i.e. pure function), it doesn't need to be on the instance
- to convert to render props API:
  - remove contents of render method
  - return `this.props.children` and call as function
  - provide state or state updaters that consumers need
- still able to create default props or commonly-used components

## prop collections

- props tht most users will want on the component can be passed and spread in the implementation, that way changes can be made without user having to update
- problem occurs when trying to pass custom methods (e.g. call another function in addition to `onToggle` in `onClick`)
