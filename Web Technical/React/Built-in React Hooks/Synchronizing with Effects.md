Some components need to synchronize with external systems.

==_Effects_== let you run some code after rendering so that you can synchronize your component with some system outside of **==React==**.

> [!info] useEffect – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/useEffect](https://react.dev/reference/react/useEffect)  

```JavaScript
import {useEffect} from 'react';

useEffect(() => { console.log('use effect ran'); }) // run everytime component re-render
```

  

> [!important] **We might not need an Effect**

**Don’t rush to add Effects to your components.** Keep in mind that Effects are typically used to “step out” of your React code and synchronize with some _external_ system.

  

> [!important] Wrapping the
> 
> ==**DOM**== update in an Effect, you let React ==update the screen first==. Then your Effect runs.

Most of the case the `useEffect` is used to work with ==**DOM**==, move an effect ==out of the rendering== calculation

### Usage

1. Connecting to an external system
2. Wrapping Effects in custom Hooks
3. Controlling a non-React widget
4. Fetching data with Effects
5. Specifying reactive dependencies
6. Updating state based on previous state from an Effect
7. Removing unnecessary object dependencies
8. Removing unnecessary function dependencies
9. Reading the latest props and state from an Effect
10. Displaying different content on the server and the client

  

> [!important] An
> 
> `Effect` lets you ==_**keep your component synchronized**_== with some external system (like a chat service). Here, ==_external system_== means any piece of code that’s **==not controlled by React==**, such as:
> 
> - Browser ==**DOM**==
> - A timer managed with `setInterval()` and `clearInterval()`.
> - An event subscription using `window.addEventListener()` and `window.removeEventListener()`
> - A third-party animation library with an API like `animation.start()` and `animation.reset()`

  

> [!important] The
> 
> `useEffect` is a very important Hook in ==**React**==

We can take a look of these example with `useEffect`

> [!info] useEffect – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/useEffect#examples-connecting](https://react.dev/reference/react/useEffect#examples-connecting)