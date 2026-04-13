---
Created by: liemgumball
Created time: 2024-06-25T17:40
tags:
  - Frontend
  - Interview
  - ReactJS
---
# What is React JS?

==**[[React]]**== is a component-based **[[JavaScript]]** library used to build reusable components for the view layer in ==**MVC**== architecture

> [!important] ==**MVC**==
> 
> is an ==architectural/design pattern== that separates an application into ==three== main logical components **Model**, **View**, and **Controller**.  
> Each architectural component is built to handle specific development aspects of an application. It ==isolates== the business, logic, and presentation layer from each other

  

## **The building blocks of React?**

- **Components:** These are reusable blocks of code that return **HTML**.
- **JSX:** It stands for ==**JavaScript**== and **XML** and allows you to write **HTML** in ==**React**==.
- **Props and State:** `props` are like function parameters and `state` is similar to variables.
- **Context:** This allows data to be passed through components as props in a hierarchy.
- **Virtual DOM:** It is a ==lightweight== copy of the actual **DOM** which ==makes== ==**DOM**== ==manipulation easier==

  

## **React Interview Questions For Freshers**

1. Differences between `props` and `state`What
    
    |`props`|`state`|
    |---|---|
    |**React** allows us to pass information to a Component using something called `props`(objects which can be used inside a component)|An instance of React Component that can be defined as an object of a set of ==observable properties== that ==control the behaviour of the component==|
    |The Data is passed from one component to another.|The Data is passed within the component only.|
    |It is Immutable (cannot be modified).|It is Mutable ( can be modified).|
    |Props can be used with state and functional components.|The state can be used only with the state components/class component (Before 16.0).|
    |Props are read-only.|The state is both read and write.|
    
2. What is ==**virtual DOM**== in **React?**
    
    **React** uses the ==**virtual DOM**== which like a lightweight copy of the actual **DOM**. So for every object that exists in the original **DOM**, there is an object for that in ==**React Virtual DOM**==. It is the same, but it does not have the power to directly change the layout of the document. Manipulating **DOM** is slow, but manipulating ==**Virtual DOM**== is fast as nothing gets drawn on the screen.
    
3. What is **JSX**?
    
    **JSX** is basically a ==syntax extension== of regular **JavaScript** and is used to ==create React elements==
    
    These elements are then rendered to the ==**React DOM**==
    
4. Types of React component
    - Functional components: are simply **JavaScript** functions
    - Class components: are a little more complex than the ==functional components==. The ==functional components== are not aware of the ==other components== in your program whereas the ==class components== can work with each other. We can pass data from one class component to another class component
5. How do Browsers read **JSX**?
    
    In general, browsers are ==not== capable of reading **JSX** and ==only== can read pure **JavaScript**.
    
    The web browsers read **JSX** with the help of a ==transpiler==. Transpilers are used to convert **JSX** into **JavaScript**. The transpiler used is called ==**Babel**==
    
6. What is `key` in **React**?
    
    A `key` is a special ==string attribute== you need to include when creating ==lists== of elements in **React**. Keys are used in **React** to identify which items in the list inside **React DOM** are changed, updated, or deleted.
    
7. What is **High-order Component**?
    
    **HOC** is the advanced method of ==reusing== the component ==functionality logic== make it’s easier to code and read
    

  

## **React Intermediate Interview Questions**

1. Conditional rendering
    
    ```JavaScript
    {isLoggedIn == false ? <DisplayLoggedOut /> : <DisplayLoggedIn />}
    ```
    
2. What is **react router**?

It is a standard ==library for routing== in **React**. It enables the ==navigation== among views of various components in a React Application, allows changing the browser **URL**, and keeps the **UI** in sync with the **URL**.

1. LifeCycle methods of Component
    
    A ==**React Component**== can go through four stages of its life as follows.
    
    - **Initialization:** This is the stage where the component is constructed with the given `props` and ==default== `state`. This is done in the `constructor` of a Component Class.
    - **Mounting:** Mounting is the stage of ==rendering== the **JSX** returned by the render method itself.
    - **Updating:** Updating is the stage when the `state` of a component is updated and the application is ==repainted==.
    - **Unmounting:** the final step of the component lifecycle where the component is removed from the page.
2. What is the use of `ref` in **React**?
    
    `Ref` is a function provided by **React** so the **Component** can interact with the ==**real DOM**==
    
3. What are **Hooks**?
    
    **Hooks** let developers use `state` and other React features without writing a class.
    
    It provide a direct API to react concepts such as `props`, `state`, `context`, `refs` and life-cycle
    
4. `useState`
    
    The most used hook in React is the `useState()` hook. It allows functional components to manipulate **DOM** elements before each render
    
5. `useEffect`
    
    It eliminates the ==side effect== of using class based components. It is used as an alternative to `componentDidUpdate()` method.
    
6. How to **CSS** in **React**?
    
    ==**CSS**== ==modules== are a way to locally scope the content of our **CSS** file. We can create a ==**CSS**== ==module== file by naming our **CSS** file as `Component.modules.css` and then it can be imported inside `Component.jsx` file
    
7. What are ==styled-components==?
    
    It’s a Module allows us to write **CSS** within **JavaScript** in a very modular and reusable way in ==**React**==. Instead of having one ==global== ==**CSS**== ==file== for a React project
    
      
    

## **React Interview Questions For Experienced**

1. What is **DRY**?
    
    It stands for **Don’t Repeat Yourself**. It helps us to write a logic once and use it anywhere in the code.
    
2. What is ==**react-redux**==?
    
    It is a ==state management tool== which makes it ==easier to pass== these `states` from one component to another irrespective of their position in the component tree and hence prevents the complexity of the application.
    
    They are several benefits of using ==react-redux== such as:
    
    - It provides ==centralized state management== i.e. a single store for whole application
    - It ==optimizes performance== as it prevents re-rendering of component
    - Makes the process of ==debugging easier==
3. What is ==axios==?
    
    It is a popular library is mainly used to send asynchronous **HTTP** requests to **REST** endpoints

## Related

- [[React]]
- [[JavaScript]]