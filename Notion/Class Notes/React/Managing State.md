
<aside>
🐞 As your application grows, it helps to be more intentional about how your state is organized and how the data flows between your components. Redundant or duplicate state is a common source of bugs.

</aside>

## Reacting to input with *State*

With **React**, we won’t modify the UI from code directly. For example, we won’t write commands like “disable the button”, “enable the button”, “show the success message”, etc. Instead, we will describe the UI you want to see for the different visual states of the component

and then trigger the state changes in response to user input. This is similar to how designers think about **UI**

## **Choosing the state structure**

<aside>
💡 Structuring state well can make a difference between a component that is pleasant to modify and debug

</aside>

The most important principle is that state shouldn’t contain redundant or duplicated information. If there’s unnecessary state, it’s easy to forget to update it, and introduce bugs!

## Principles for structuring *State*

1. **Group related state.** If we always update two or more state variables at the same time, consider merging them into a single state variable.
    
    ```jsx
    // bad
    const [x, setX] = useState(0);
    const [y, setY] = useState(0);
    
    //good
    const [position, setPosition] = useState({ x: 0, y: 0 });
    ```
    
2. **Avoid contradictions in state.** When the state is structured in a way that several pieces of state may contradict and “disagree” with each other, you leave room for mistakes. Try to avoid this.
    
    ```jsx
    //bad
    // this make contradiction if isSending and isSent are true as the same time
    const [text, setText] = useState('');
    const [isSending, setIsSending] = useState(false); // contradiction
    const [isSent, setIsSent] = useState(false); // contradiction
    
    //good
    const [text, setText] = useState('');
    const [status, setStatus] = useState('typing'); // can be isSending or isSent
    ```
    
3. **Avoid redundant state.** If you can calculate some information from the component’s props or its existing state variables during rendering, you should not put that information into that component’s state.
    
    ```jsx
    const [firstName, setFirstName] = useState('');
    const [lastName, setLastName] = useState('');
    //bad
    const [fullName, setFullName] = useState(''); //no needed
    ```
    
4. **Avoid duplication in state.** When the same data is duplicated between multiple state variables, or within nested objects, it is difficult to keep them in sync. Reduce duplication when you can.
    
    ```jsx
    const initialItems = [
      { title: 'pretzels', id: 0 },
      { title: 'crispy seaweed', id: 1 },
      { title: 'granola bar', id: 2 },
    ];
    
    // bad
    export default function Menu() {
      const [items, setItems] = useState(initialItems);
      const [selectedItem, setSelectedItem] = useState(items[0]); // duplication
    }
    
    //good
    export default function Menu() {
      const [items, setItems] = useState(initialItems);
      const [selectedId, setSelectedId] = useState(0); // no duplication
    }
    ```
    
5. **Avoid deeply nested state.** Deeply hierarchical state is not very convenient to update. When possible, prefer to structure state in a flat way.
    
    [Choosing the State Structure – React](https://react.dev/learn/choosing-the-state-structure#avoid-deeply-nested-state)