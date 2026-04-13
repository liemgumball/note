---
Created: 2023-08-28T08:58
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://legacy.reactjs.org/docs/getting-started.html
Reviewed: true
Edited: 2025-05-10T14:46
---
> [!important] ==**React**==
> 
> is a ==**JavaScript**== library for building user interfaces.
> 
> ==**React**== is used to build single-page applications.
> 
> ==**React**== allows us to create reusable UI components.

  

## Here is my example

https://github.com/liemgumball/internship_AlgilityIO/pull/9

# **How does React Work?**

> [!important] React creates a ==**VIRTUAL DOM**== in memory.

Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.

  

> [!important] React only changes what needs to be changed!

  

# Getting started

## Required

- [[JavaScript]]
- Install ==**[nvm](https://github.com/nvm-sh/nvm#install--update-script)**== and ==[**Node.js**](https://nodejs.org/en/download/)== **v.16**

## Create a simple React app

```Bash
npx create-react-app my-app
```

Install and run on local

```Bash
cd my-app
npm start
```

# Basic

[[Installation]]

## Components

[[Thinking in React]]

## Re-Rendering

[[Re-rendering and Commit]]

## Handling Events

[[Responding to Events]]

## State: A Component’s Memory

[[State and Lifecycle]]

## **Series of State Updates**

[[Queueing a Series of State Updates]]

## Managing State

[[Managing State]]

## React Hooks

[[Built-in React Hooks]]

---

## ==Bookmark Reference==

https://github.com/kettanaito/naming-cheatsheet

https://github.com/TobitSoftware/react-project-guideline

> [!info] How to Improve Your ReactJS Code – Tips for Code Readability and Performance  
> ReactJS is one of the most popular JavaScript libraries for building scalable and performant applications.  
> [https://www.freecodecamp.org/news/improve-reactjs-code/](https://www.freecodecamp.org/news/improve-reactjs-code/)  

# Open Questions

1. What are differences between class components and functional components?
    
    Here some main differences between _==Class Components==_ and _==Functional Components==_
    
    ||Class Components|Functional components|
    |---|---|---|
    |**Syntax**|`class MyComponent extends React.Component`|`function MyComponent(props)`|
    |**State Management**|using `**this.state**` **and lifecycle methods**|using Hooks|
    |**Hooks**|don’t use Hooks. Rely on Lifecycle methods|Hooks were introduced primarily for functional components.|
    
      
    
2. What makes a component to re-render?
    
    - States changed
    - Props changed
    - Contexts changed
    - Parent Component re-render
    
      
    
3. What are differences between ==_state_== and ==_prop_== in React?
    
    - ==**Props**==**:** used to pass data from a parent components to a child component, ==managed by parent component==. This means that we ==cannot== change it within that child component
    - ==**State**==: used to manage and store date within that ==own component==, and can be changed to ==trigger a re-render== of the component
    
      
    
4. What’s the key in list?
    
    In ==**React**==, when we render a list of items using JSX, it is a common practice to assign a ==unique== `key` prop to each item in the list
    
    The `key` prop is a special attribute that helps React identify individual elements in a list and ==_optimize the rendering process_==
    
      
    
5. What’s lifting state up?
    
    ==**Lifting state up**== is a common pattern in React where we move the state of a component higher up the parent component to share state between two or many components.
    
    ```JavaScript
    function Parent() {
    	const [count, setCount] = useState(0)
    
    	return (
    		<>
    			<p>Count: {count}</p>
          <Child count={count} setCount={setCount} /> //lifting state up
    		</>
    	)
    }
    ```
    
      
    
6. What is the use of `useEffect`?
    
    `**useEffect**` is a hook in React that allows you to perform ==side effects== in function components
    
    It helps maintain a clean and declarative way to ==handle asynchronous tasks== and ==interactions outside of the component rendering process==
    
    **Usage:**
    
    - Data Fetching
    - DOM manipulation
    - Reacting to State or Prop Changes
    - Component clean up
    
      
    
7. What’s the importance of the dependency array in hooks? Make example for some cases: missing/empty/include dependency and use clean up function in hook.
    
    The ==_dependency array in React hooks_==, such as `**useEffect**`, is a crucial aspect of managing the behaviors and side effects of your components. It specifies which ==variables== or ==values== the ==effect depends on==, and it controls when the effect runs and how it ==reacts to dependency’s changes==
    
    - **Missing**: runs on every render
    
    ```JavaScript
    function Example() {
      const [count, setCount] = useState(0);
    
      useEffect(() => {
        console.log('Effect ran'); // this run every render
      });
    
      return (
    		<>
    			<p>Count: {count}</p>
          <button onClick={() => setCount(c => c + 1)}>Increment</button>
    		</>
      );
    }
    ```
    
    - **Empty:** runs once when the component mounts
    
    ```JavaScript
      useEffect(() => {
        console.log('Effect ran'); // run one time when the component mounts
      }, []);
    ```
    
    - **Include dependency:** runs if the dependencies changed
    
    ```JavaScript
      useEffect(() => {
        console.log('Effect ran'); // run one time when the component mounts
      }, [count]);
    ```
    
      
    
8. What is the use of `useRef`?
    
    `**useRef**` is a hook in React that provides a way to create ==mutable references to DOM elements== or to ==store== ==mutable values==
    
    **Usage:**
    
    - **Accessing DOM Elements**
    - **Storing Mutable Values**
    - **Managing Mutable State in Custom Hooks** (for example: used to store the latest `callback function` in custom hook)
    
      
    
9. When should you use `useCallback`, `useMemo`?
    
    They are used to ==prevent== unnecessary ==re-computation== and ==re-renders== by memorizing values and functions.
    
    - `**useCallback**` used when we want to memorize a function to prevent it from being recreated on every render
    - `**useMemo**` used when we want to memorize the result of a computation or a value, prevent the re-computation on every render