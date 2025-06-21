Usually, you will pass ==information== from a parent component to a child component ==via props==. But passing props can become ==verbose== and ==inconvenient== if you have to pass them through many components in the middle, or if ==many== components in your app ==need== the ==same information==. **_Context_** lets the parent component make some information available to any component in the tree below it—==no matter how deep==—without passing it explicitly through props.

> [!info] Passing Data Deeply with Context – React  
> The library for web and native user interfaces  
> [https://react.dev/learn/passing-data-deeply-with-context](https://react.dev/learn/passing-data-deeply-with-context)  

## **The problem with passing props**

![[Web Technical/React/Built-in React Hooks/Passing Data Deeply with Context/attachments/Untitled.png|Untitled.png]]

Lifting state up

  

![[Web Technical/React/Built-in React Hooks/Passing Data Deeply with Context/attachments/Untitled 1.png|Untitled 1.png]]

Prop drilling

```JavaScript
import Heading from './Heading.js';
import Section from './Section.js';

export default function Page() {
  return (
    <Section>
      <Heading level={1}>Title</Heading>
      <Section>
        <Heading level={2}>Heading</Heading>
        <Heading level={2}>Heading</Heading>
        <Heading level={2}>Heading</Heading>
        <Section>
          <Heading level={3}>Sub-heading</Heading>
          <Heading level={3}>Sub-heading</Heading>
          <Heading level={3}>Sub-heading</Heading>
          <Section>
            <Heading level={4}>Sub-sub-heading</Heading>
            <Heading level={4}>Sub-sub-heading</Heading>
            <Heading level={4}>Sub-sub-heading</Heading>
          </Section>
        </Section>
      </Section>
    </Section>
  );
}
```

## _**Context**_**: an alternative to passing props**

1. **Create** a context. (We can call it `LevelContext`, since it’s for the heading level.)
    
    ```JavaScript
    import { createContext } from 'react';
    
    export const LevelContext = createContext(1);
    ```
    
2. **Use** that context from the component that needs the data. (`Heading` will use `LevelContext`.)
    
    ```JavaScript
    import { useContext } from 'react';
    import { LevelContext } from './LevelContext.js';
    ```
    
    ```JavaScript
    export default function Heading({ children }) {
      const level = useContext(LevelContext);
      // ...
    }
    ```
    
3. **Provide** that context from the component that specifies the data. (`Section` will provide `LevelContext`.)
    
    ```JavaScript
    import { LevelContext } from './LevelContext.js';
    
    export default function Section({ level, children }) {
      return (
        <section className="section">
          <LevelContext.Provider value={level}>
            {children}
          </LevelContext.Provider>
        </section>
      );
    }
    ```
    

![[Web Technical/React/Built-in React Hooks/Passing Data Deeply with Context/attachments/Untitled 2.png|Untitled 2.png]]

Using context in close children

![[Web Technical/React/Built-in React Hooks/Passing Data Deeply with Context/attachments/Untitled 3.png|Untitled 3.png]]

Using context in distant children

## **Using and providing context from the same component**

> [!info] Passing Data Deeply with Context – React  
> The library for web and native user interfaces  
> [https://react.dev/learn/passing-data-deeply-with-context#using-and-providing-context-from-the-same-component](https://react.dev/learn/passing-data-deeply-with-context#using-and-providing-context-from-the-same-component)  

## **Context passes through intermediate components**

You can insert as many components as you like between the component that provides context and the one that uses it. This includes both built-in components like `<div>` and components you might build yourself.