Created: July 18, 2024 12:40 PM
Class: Self-Research
Type: Front-end
Materials: https://redux.js.org/tutorials/essentials/part-1-overview-concepts
Reviewed: No
Edited: December 3, 2024 11:15 AM

<aside>
📌 **Redux** is a **JS** library for predictable and maintainable global state management.

</aside>

It helps you write applications that behave consistently, run in different environments *(client, server, and native)*, and are easy to test.

## Getting started

[Getting Started with Redux | Redux](https://redux.js.org/introduction/getting-started)

## Installation

**Redux core**

```bash
npm install redux
```

**Redux Toolkit**

```bash
npm install @reduxjs/toolkit
```

**Redux Example App**

```bash
# Vite with our Redux+TS template
# (using the `degit` tool to clone and extract the template)
npx degit reduxjs/redux-templates/packages/vite-template-redux my-app
```

# What is Redux?

**Redux is a pattern and library for managing and updating application state, using events called "*actions*".** It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring that the state can only be updated in a predictable fashion.

**Redux** is more useful when:

- You have large amounts of application state that are needed in many places in the app
- The app state is updated frequently over time
- The logic to update that state may be complex
- The app has a medium or large-sized codebase, and might be worked on by many people

[frontend-training/Redux at redux · liemgumball/frontend-training](https://github.com/liemgumball/frontend-training/tree/redux/Redux)

## Key concepts of Redux

[Three Principles | Redux](https://redux.js.org/understanding/thinking-in-redux/three-principles)

1. Store and States (Slices)
    
    The center of every **Redux** application is the **store**. A `store` is a container that holds your application's global **state**.
    
2. Actions and Reducers
    
    Reducer is like a state-driver based on which `action` is called.
    
    An action is an object representing how we handling the state in store *(the `type` key in `action` will define)* 
    
3. Action creators
4. Subscription
5. Selectors
6. Combined states (slices)
7. Middleware
    
    ```tsx
    storeAPI => next => action => {
    	// do some logics
    	// ...
    	const returnValue = next(action)
    	
    	// do some logics
    	// ...
    	
    	return returnValue
    }
    ```
    
8. Async actions with **Redux Thunk** or  **Redux Saga**

---

# Redux Saga

[Redux Saga](Redux%20Saga.md)

---

# Redux Toolkit

[Redux Toolkit | Redux Toolkit](https://redux-toolkit.js.org/)

<aside>
💡 **Redux** **Toolkit** is the recommended approach for writing **Redux** logic.
It contains packages and functions that we think are essential for building an app.

</aside>

**Redux Toolkit** builds in suggested best practices, simplifies most **Redux** tasks, prevents common mistakes, and makes it easier to write applications.

# Style Guide

[Style Guide | Redux](https://redux.js.org/style-guide/)