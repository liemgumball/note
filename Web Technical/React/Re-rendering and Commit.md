> [!important] Before your components are displayed on screen, they must be rendered by React.

  

Imagine that your ==components== are cooks in the kitchen, assembling tasty dishes from ==ingredients==. In this scenario, React is the ==waiter== who puts in requests from customers and brings them their orders.

1. ==**Triggering**== a render (delivering the guest’s order to the kitchen)
    - It’s the component’s ==**initial render**==**.**
    - The component’s (or one of its ancestors’) ==**state has been updated**==**.**
2. ==**Rendering**== the component (preparing the order in the kitchen)
    - ==**On initial render**==**,** React will call the root component.
    - ==**For subsequent renders**==**,** React will call the function component whose state update triggered the render.
3. ==**Committing**== to the real ==**DOM**== (placing the order on the table)
    - ==**For the initial render**==**,** React will use the [`appendChild()`](https://developer.mozilla.org/docs/Web/API/Node/appendChild) **DOM API** to put all the **DOM** nodes it has created on screen.
    - ==**For re-renders**==**,** React will apply the ==minimal necessary operations== (calculated while rendering!) to make the **DOM** match the latest rendering output.