Setting a state variable will ==queue== another render. But sometimes you might want to perform multiple operations on the value ==before queueing the next render==. To do this, it helps to understand how React ==_batches_== state updates.

  

## **React batches state updates**

```JavaScript
export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 1);
        setNumber(number + 1);
        setNumber(number + 1);
      }}>+3</button>
    </>
  )
}

// onclick => +1
```

  

However, as you might recall from the previous section, [each render’s state values are fixed](https://react.dev/learn/state-as-a-snapshot#rendering-takes-a-snapshot-in-time), so the value of `number` inside the first render’s event handler is always `0`, no matter how many times you call `setNumber(1)`:

```JavaScript
setNumber(0 + 1);
setNumber(0 + 1);
setNumber(0 + 1);
```

  

This lets you update multiple state variables—even from multiple components—without triggering too many ==re-renders.== But this also means that the UI won’t be updated until _after_ your event handler, and any code in it, completes. This behavior, also known as ==**batching**==

## **Updating the same state multiple times before the next render**

> [!important] It is an
> 
> ==uncommon== use case, we can pass a _function_ that calculates the next state based on the previous one in the queue, like `setNumber(n => n + 1)`

It is a way to tell React to _“do something with the state value”_ ==instead== of just replacing it.