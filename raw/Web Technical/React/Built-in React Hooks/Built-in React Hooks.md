**_Hooks_** let you use different ==**[[React]]**== features from your components. You can either use the ==built-in Hooks== or combine them to ==build your own==

# Rules of Hooks

1. ==**Only call Hook at a Top Level:**== Don’t call Hooks inside loops, conditions, or nested functions
2. ==**Only Call Hooks from React Functions:**== Don’t call Hooks from a Regular JavaScript functions
3. ==**ESLint Plugin**==
    
    > [!info] Rules of Hooks – React  
    > A JavaScript library for building user interfaces  
    > [https://legacy.reactjs.org/docs/hooks-rules.html#eslint-plugin](https://legacy.reactjs.org/docs/hooks-rules.html#eslint-plugin)  
    

# Must Know Hooks

## State Hooks

To add state to a component, use one of these Hooks:

- `useState` declares a state variable that you can update directly.
- `useReducer` declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)
    - The `useReducer` Hook takes two arguments:
        1. A reducer function
        2. An initial state
    - And it returns:
        1. A stateful value
        2. A dispatch function (to “dispatch” user actions to the reducer)

**Comparing** `**useState**` **and** `**useReducer**`

> [!info] Extracting State Logic into a Reducer – React  
> The library for web and native user interfaces  
> [https://react.dev/learn/extracting-state-logic-into-a-reducer#comparing-usestate-and-usereducer](https://react.dev/learn/extracting-state-logic-into-a-reducer#comparing-usestate-and-usereducer)  

## **Context Hook**

_Context_ lets a component **==receive information from distant parents without passing it as props.==**

> [!info] useContext – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/useContext](https://react.dev/reference/react/useContext)  

[[Passing Data Deeply with Context]]

## Ref Hook

You can access the current value of that ref through the `ref.current` property.

When you want a component to “remember” some information, but you don’t want that information to ==**trigger new renders**==, you can use a ==_ref_==.

```JavaScript
import { useRef } from 'react';

const ref = useRef(0);
```

`useRef` returns an object like this:

  

```JavaScript
{ 
  current: 0 // The value you passed to useRef
}
```

  

### **Refs and the DOM**

We can point a ref to any value. However, the most common use case for a ref is to access a ==**DOM**== element. For example, this is handy if you want to focus an input programmatically. When you pass a ref to a `ref` attribute in JSX, like `<div ref={myRef}>`, React will put the corresponding ==**DOM**== element into `myRef.current`

> [!important] Read more about this in
> 
> **==[Manipulating the DOM with Refs.](https://react.dev/learn/manipulating-the-dom-with-refs)==**

[https://gist.github.com/liemgumball/42a1d083e158a06d40a2fe2f0f73af06](https://gist.github.com/liemgumball/42a1d083e158a06d40a2fe2f0f73af06)

  

### **Differences between refs and state**

In most cases, you’ll want to use state. Refs are an “_==escape hatch==_” you won’t need often.

|refs|state|
|---|---|
|`useRef(initialValue)` returns `{ current: initialValue }`|`useState(initialValue)` returns the current value of a state variable and a state setter function `( [value, setValue])`|
|==Doesn’t== trigger ==re-render== when you change it.|Triggers ==re-render== when you change it.|
|Mutable—you can modify and update current’s value outside of the rendering process.|“Immutable”—you must use the state setting function to modify state variables to queue a re-render.|
|You shouldn’t read (or write) the current value during rendering.|You can read state at any time. However, each render has its own snapshot of state which does not change.|

## Effect Hook

[[Synchronizing with Effects]]

## Lesser Used Hooks

- `useMemo`: cache the result of a calculation between re-renders
    
    > [!info] useMemo – React  
    > The library for web and native user interfaces  
    > [https://react.dev/reference/react/useMemo](https://react.dev/reference/react/useMemo)  
    
- `useCallback`: cache a function definition between re-renders
    
    > [!info] useCallback – React  
    > The library for web and native user interfaces  
    > [https://react.dev/reference/react/useCallback](https://react.dev/reference/react/useCallback)  
    
- `useReducer`
    
- `useTransition`: update the state without blocking the UI
    
    > [!info] useTransition – React  
    > The library for web and native user interfaces  
    > [https://react.dev/reference/react/useTransition](https://react.dev/reference/react/useTransition)  
    
    Preventing unwanted loading re-render of ==_lower priority State_==
    
- `useDeferredValue`: defer updating a part of the UI
    
    ```JavaScript
    import { useDeferredValue, useState, useEffect } from 'react'
    
    function App() {
    	const [input, setInput] = useState("")
    
    	return (
    		<input type="text" value={input} onChange={(e) => setInput(e.target.value)} />
    		<List input={input} />
    	)
    }
    
    function List({ input }) {
    	const deferredInput = useDeferredValue(input)
    
    	useEffect( () => {
    		console.log(`input: ${input}\ndeferred: ${deferredInput}`)
    	}, [input, deferredInput])
    }
    ```
    
    This means if the `input` changed multiple times instantly. ==**React**== will wait until there is ==no changes== of `input` in a few milliseconds, the `deferredInput` will be updated.
    

## Optional Hooks

- `useLayoutEffect`: same as `useEffect` (run after DOM being re-render) but it runs _synchronously_ when ==**React**== calculating and re-render the **==DOM==**
- `useDebugValue`: add a label to a custom Hook in **==React DevTools==**
- `useImperativeHandle`: customize the handle exposed as a `ref`. We can create many handle options inside a component with its `ref`
- `useId`: generating unique IDs that can be passed to _accessibility attributes (_`_id_`_,_ `_name_`_, ... )_

## Custom Hooks

We can also create our ==_own Hooks_== for the application’s needs

> [!important] Hook names always start with
> 
> `use`

### **Custom Hooks: Sharing logic between components**

> [!important] ==**Custom Hooks**==
> 
> let you share `_stateful_` _logic_ but ==not== _state itself._ Each call to a Hook is completely independent from every other call to the same Hook.

1. Passing reactive values between Hooks
2. Passing event handlers to custom Hooks

> [!important] We don’t need to extract a custom Hook for every little duplicated code.
> 
>   
> _Some duplication is fine_

However, wherever we write an ==**Effect**==, consider whether it would be clearer to wrap in a **==custom Hook==**

> _We shouldn’t need Effects very often_

So if we’re writing one, its mean that we need to **==_step outside React_==** to synchronize with some external system.

## Related
- [[React]]
- [[State and Lifecycle]]
- [[Synchronizing with Effects]]
- [[Passing Data Deeply with Context]]