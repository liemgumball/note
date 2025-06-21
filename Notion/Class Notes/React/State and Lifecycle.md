==**State**== is similar to ==props==, but it is ==private== and ==fully controlled== by the component.

  

Components often need to change what’s on the screen as a result of an interaction. In React, this kind of component-specific memory is called ==_state_==.

The component will re-render itself if their _==state==_ changed

## Lifecycle Methods ==(out dated)==

- Mounting Phase:
    - `**constructor(props)**`
    - `**static getDerivedStateFromProps(props, state)**`**:** Rarely used
    - `render`
- Updating Phase:
    - `**static getDerivedStateFromProps(props, state)**`: Similar to the mounting phase, used to update state based on new props.
    - `**shouldComponentUpdate(nextProps, nextState)**`: Determines if the component should re-render, based on changes in props or state.
    - `**render()**`
- Unmounting Phase:
    - `**componentWillUnmount()**`: Invoked before a component is removed from the DOM. Used for clean up tasks.
- Error Handling Phases:
    - `**static getDerivedStateFromError(error)**`: Used to render a fall-back UI when an error occurs during rendering.
    - `**componentDidCatch(error, info)**`: Used to log error information.

  

> [!important] Developers prefer use React Hooks now than Lifecycle methods

  

## Updating Objects in State

==_State_== can hold any kind of ==**JavaScript**== value, including objects. But you shouldn’t change objects that you hold in the ==**React**== state directly. Instead, when you want to update an object, you need to create a new one (or ==make a copy of an existing one==), and then set the state to ==use that copy==.

```JavaScript
const [position, setPosition] = useState({ x: 0, y: 0 });

position.x = 5; positin.y = 10; //won't work
setPosition({x: 5, y: 10}) // create an object and set a copy of it
```

  

## Updating Arrays in State

_==Arrays==_ are mutable in ==**JavaScript**==, but you should treat them as immutable when you store them in state. Just like with objects, when you want to update an array stored in state, you need to create a new one (==or make a copy of an existing one==), and then set state to ==use the new array==.

```JavaScript
const [items, setItems] = useState([]);

items.push({id: 1, name:'1'}); //won't work

setItems([...items, {id:1, name:'1'}]) //create new array and set a copy of it
```