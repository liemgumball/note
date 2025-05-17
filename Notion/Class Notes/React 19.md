Created: January 8, 2025 7:50 PM
Class: Self-Research
Type: Front-end
Materials: https://react.dev/blog/2024/12/05/react-19
Reviewed: No
Edited: January 11, 2025 9:48 AM

# Why React?

Why we talk about React? (*this is to explain why we have a topic about React)*

1. mgm is using React 😊
2. React is a rock start in web development! 🤩
    
    A bit about history ⇒ create by Facebook … (some images of core team members)
    
    [Technology | 2024 Stack Overflow Developer Survey](https://survey.stackoverflow.co/2024/technology#1-web-frameworks-and-technologies)
    
    Following the 2024 Stack Overflow survey, React has blown past **JQuery** to become the most commonly used web framework 🤯
    
    ![image.png](Notion/Class%20Notes/React%2019/image.png)
    

1. The component based architecture
    1. Reusable components for elements like buttons, menus, or entire page sections
    2. Piece them together like building blocks to create user interfaces 🧩
    3. Makes development faster while improving reusability and maintainability 👍
2. 
3. JSX
    1. Write HTML-like code directly in JavaScript 😎
    2. Don't have to constantly switch between HTML and JavaScript files 
4. Super fast with Virtual DOM
    1. Lightweight representation of the actual webpage structure
    2. It determines the most efficient way to update the webpage and only applies those specific changes
5. The community …

<aside>
<img src="https://www.notion.so/icons/book-closed_gray.svg" alt="https://www.notion.so/icons/book-closed_gray.svg" width="40px" />

Conclusion of the first part:

Since first come to the development world in 2012, it makes writing code to user interface for the a web site smoothly than even

> *Make a small joke to create exciting*
> 

From this (old code of html file and javascript file using JQuery)

To This ⇒ `render( <App /> )`

</aside>

---

# React 19

*This is the main section*

React got a major update in the version 19. Many of these features were introduced as experimental in React 18, but they will be marked as stable in React 19.

But before you (audience) wonder how long it will take you to learn this new version of React. I have some good news.

<aside>
📌

Bring up small hint about what developer will achieve when using React 19

</aside>

React 19 is:

- Less about the code you have to write
- More about the code you don’t have to write anymore

Why i’m saying that? Take a look of this (*show some difference of code or image)*

| Before | After |
| --- | --- |
| `useCallback` , `useMemo`, `memo`, `forwardRef` | Clean 🧹🥳 |

This can help you build your React project faster.

## React compiler 🛠️

The biggest part of the new version in React Compiler, this is the reason why we can achieve every thing i mentioned above. Most of the feature in React 19 are due to the React Compiler.

### What does it do?

It’s called “compiler”, so basically it converts your React code into regular JavaScript code 😃.

### But why this is so important?

For a longtime, React only ran in the browser and there is no compile step at all.

Others framework like **Svelt** or **Astro** has their own compiler already. This compiler step taking of a lot of things for you behind the scene so you don’t have to write extra code.

![image.png](image%201.png)

But React never have it 🙂, that why we have different of hooks API like `useCallback` `useMemo` `memo` to manually improve performance things.

These hooks are all necessary to prevent unnecessary re-renders. But there are hard to use properly, even if you have some tool to remind you like `wdyr` .

All of this just to make sure your webpage run performantly, because it was no compiler to do that for you automatically.

![image.png](image%202.png)

To simplify, he main benefit of this is to improve your overall app performance, but the best part is it removes the need for you 🤔 to think as much about performance 🙅‍♂️.

Now, the new compiler optimize your react code automatically, so you can completely remove any performance hooks. 

![image.png](image%203.png)

… *deep diving into React compiler* 👍

---

It gets even better, we also no longer need to use the `forwardRef` function. (*connect to the next section)*

### Get rid of `forwardRef`

![image.png](image%204.png)

To this

![image.png](image%205.png)

We can access to `ref` as a prop, which is a really nice improvement. I think Widget team will like this 😄

<aside>
💡

This remove of the `forwardRef` does not mean your code will be shorter. But there will be less thing to worry about when writing React code.

</aside>

Also provide cleanup as returned function for `React.Ref` (similar to cleanup in `useEffect`)

But this small change may lead to some breaking code cause since React 19, any return from `ref` is not a function will be rejected by Typescript.

### There’s even more React code to remove

New `use` hook 🪄

- Lets you load resources asynchronously
    - `promises`
    - `contexts`

It can replace 2 major hooks

- Replace `useEffect` for things like data fetching 😦
    
    ![image.png](image%206.png)
    
    To this
    
    ![image.png](image%207.png)
    
    This is a lot cleaner to read 🧹👍 (`Suspense` is React 18 feature allows you stream things)
    
- Replace `useContext` for reading context
    
    ![image.png](image%208.png)
    
    To this
    
    ![image.png](image%209.png)
    
    Just replace `useContext` by `use` 
    
    Context can be use liked its on Provider which is a really nice thing to have
    

### `use` can be used conditionally

All about the **Rule of Hook** you will be thrown out of the window with this new `use` hook

(*an image of Rule of Hook be thrown into trash bin)* 🗑️

You can run the `use` hook inside an `if` statement.

![image.png](image%2010.png)

---

## What are others new?

### Asynchronous transition

React’s adding support of using async functions in transition 

### Actions

A common use case in React apps is to perform a data mutation and then update state in response.

<aside>
💡

**By convention, functions that use async transitions are called “Actions”.** 

</aside>

![For example, when a user submits a form to change their name, you will make an API request, and then handle the response.](image%2011.png)

For example, when a user submits a form to change their name, you will make an API request, and then handle the response.

Now we can use the `useTransaction` hook to handle pending status

… *make some demo code to test transaction inside of transaction ⇒ to explain how it works following the React Conf 2024 video*

### New `useActionState`

Handling form has all been my pain in the ass 😭 since I first learning React. …

… *show some ugly code of create many state for every form element*

I always prefer using external libraies for handling form like `useFormHook` …

But React has its own hook to work with form.

… *make some demo code also using `useFormState` hook*

### `useOptimistic` hook

This hook has been introduced in React 18 but marked as experimental ⇒ now no longer

… *small demo chat box, showing sending message and sent message*

---

# Server Components

IMO, Server component is one of the biggest chance to React since it initial release 10 year ago🤩

Server Side Rendering (SSR) or Server Component
You might have heard about them 🤔 or you might have used them in frameworks like NextJS, Remix etc. Contrary to what it might seem, server components are not specifically a NextJS’s feature 😄, they are actually React feature and NextJS and Remix are the first ones to properly implement them.

- Improve page load times
- Code portability: let developers write components that can run on both the server and client
- SEO: allows search engines and LLMs to crawl and index content more effectively, improving search engine optimization.

1. Explain the difference
    
    This made a quite big news in the React community because SC are fundamentally different to how Client Components work and how we were building React app all of this time 📌
    
    Traditionally, React applications were mostly run on the client machine, which mean to the app running, the browser would have to download the Javascript bundle contain all of the code for the app to be able to run.
    
    ```html
    <!DOCTYPE html>
    <html>
      <body>
        <div id="root"></div>
        <script src="/static/js/bundle.js"></script>
      </body>
    </html>
    ```
    
    The linked script includes everything about your React application, third-party dependencies, and all your application code. As your application grew, so did your bundle size.
    
2. 

---

## Improvement

### Suspense

[React 19 Upgrade Guide – React](https://react.dev/blog/2024/04/25/react-19-upgrade-guide#improvements-to-suspense)

There was a small drama with suspensed sibling components, React 19 improve it.

### Hydration Error

Better error log

![image.png](image%2012.png)

### Support Document Metadata & stylesheets & async script

![image.png](image%2013.png)

![image.png](image%2014.png)

### Support preloading resources