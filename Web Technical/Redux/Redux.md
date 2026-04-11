---
Created: 2024-07-18T12:40
Class: Self-Research
Type: Front-end
Materials:
  - https://redux.js.org/tutorials/essentials/part-1-overview-concepts
Reviewed: false
Edited: 2024-12-03T11:15
---
> [!important] ==**Redux**==
> 
> is a ==**[[JavaScript]]**== library for predictable and maintainable global state management.

It helps you write applications that behave consistently, run in different environments _(client, server, and native)_, and are easy to test.

  

## Getting started

> [!info] Getting Started with Redux | Redux  
> Introduction > Getting Started: Resources to get started learning and using Redux  
> [https://redux.js.org/introduction/getting-started](https://redux.js.org/introduction/getting-started)  

## Installation

**Redux core**

```Bash
npm install redux
```

**Redux Toolkit**

```Bash
npm install @reduxjs/toolkit
```

**Redux Example App**

```Bash
# Vite with our Redux+TS template
# (using the `degit` tool to clone and extract the template)
npx degit reduxjs/redux-templates/packages/vite-template-redux my-app
```

  

# What is ==Redux==?

==**Redux**== **is a pattern and library for managing and updating application state, using events called "**_**actions**_**".** It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a predictable fashion.

==**Redux**== is more useful when:

- You have large amounts of application state that are needed in many places in the app
- The app state is updated frequently over time
- The logic to update that state may be complex
- The app has a medium or large-sized codebase, and might be worked on by many people

> [!info] frontend-training/Redux at redux · liemgumball/frontend-training  
> Contribute to liemgumball/frontend-training development by creating an account on GitHub.  
> [https://github.com/liemgumball/frontend-training/tree/redux/Redux](https://github.com/liemgumball/frontend-training/tree/redux/Redux)  

## Key concepts of ==Redux==

> [!info] Three Principles | Redux  
> Introduction > Three Principles: Three key principles for using Redux  
> [https://redux.js.org/understanding/thinking-in-redux/three-principles](https://redux.js.org/understanding/thinking-in-redux/three-principles)  

1. Store and States (Slices)
    
    The center of every **Redux** application is the **store**. A `store` is a container that holds your application's ==global== ==**state**==.
    
2. Actions and Reducers
    
    Reducer is like a ==state-driver== based on which `action` is called.
    
    An action is an object representing how we handling the state in store _(the `type` key in `action` will define)_
    
3. Action creators
4. Subscription
5. Selectors
6. Combined states (slices)
7. Middleware
    
    ```TypeScript
    storeAPI => next => action => {
    	// do some logics
    	// ...
    	const returnValue = next(action)
    	
    	// do some logics
    	// ...
    	
    	return returnValue
    }
    ```
    
8. Async actions with **Redux Thunk** or **Redux Saga**

  

---

# ==Redux Saga==

[[Redux Saga]]

---

# Redux Toolkit

> [!info] Redux Toolkit | Redux Toolkit  
> The official, opinionated, batteries-included toolset for efficient Redux development  
> [https://redux-toolkit.js.org/](https://redux-toolkit.js.org/)  

  

> [!important] **Redux Toolkit**
> 
> is the recommended approach for writing ==**Redux**== logic.  
> It contains packages and functions that we think are essential for building an app.  

==**Redux Toolkit**== builds in suggested best practices, simplifies most **Redux** tasks, prevents common mistakes, and makes it easier to write applications.

# Style Guide

> [!info] Style Guide | Redux  
> Redux Style Guide: recommended patterns and best practices for using Redux  
> [https://redux.js.org/style-guide/](https://redux.js.org/style-guide/)

## Related
- [[React]]
- [[JavaScript]]
- [[Redux Saga]]
- [[State and Lifecycle]]