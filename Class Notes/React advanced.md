---
Created: 2023-10-10T09:22
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://legacy.reactjs.org/docs/accessibility.html#:~:text=MAIN%20CONCEPTS-,ADVANCED%20GUIDES,-Accessibility
  - https://tanstack.com/query/v3/
  - https://reactjs.org/docs/testing.html
Reviewed: true
Edited: 2025-05-10T14:46
---
> [!important] In this note, we’ll go through the
> 
> _Advanced guides_ in ==**React**==

## Accessibility

Web accessibility is the design and creation of websites that can be used by everyone.

### Standards and Guidelines

> [!info] WCAG 2 Overview  
> Introduces the Web Content Accessibility Guidelines (WCAG) international standard, including WCAG 2.  
> [https://www.w3.org/WAI/intro/wcag](https://www.w3.org/WAI/intro/wcag)  

> [!info]  
>  
> [https://www.w3.org/WAI/intro/aria](https://www.w3.org/WAI/intro/aria)  

### Semantic HTML

> [!important] Semantic
> 
> ==**HTML**== is the foundation of ==accessibility== in a web application. Using the various HTML elements to r==_einforce the meaning of information_== in our websites will often give us accessibility for free.

Sometimes we break HTML semantics when we add `<div>` elements to our JSX to make our React code work

In these cases we should rather use ==**React Fragments**== to group together multiple elements.

```TypeScript
return (
    <Fragment>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </Fragment>
  );

// or
return (
    <>
      <dt>{item.term}</dt>
      <dd>{item.description}</dd>
    </>
  );
```

### **Accessible Forms**

- Labeling
    
    Every HTML form control, such as `<input>` and `<textarea>`, needs to be labeled accessibly. We need to provide descriptive labels that are also exposed to screen readers.
    
- Notifying the user of errors
    
    Error situations need to be understood by all users.
    

### **Other Points for Consideration**

- **Focus Control**
- **Mouse and pointer events**
- **Setting the language**
- **Setting the document title** `**<title>**`
- **The keyboard**

---

## Code-Splitting

> [!important] Most
> 
> **==React==** apps will have their files “bundled” using tools like ==**[Webpack](https://webpack.js.org/)**====  
>   
> ==_**==Bundling==**_ ==is the process of following imported files and merging them into a single file==

> [!info] Code Splitting | webpack  
> webpack is a module bundler.  
> [https://webpack.js.org/guides/code-splitting/](https://webpack.js.org/guides/code-splitting/)  

### **Code-Splitting** is a feature supported by bundlers

Which can create multiple bundles that can be ==_dynamically loaded at runtime_==.

It can help ==_“lazy-load”_== just the things that are currently needed by the user, which can dramatically improve the performance of the app.

### Dynamic `import()`

```JavaScript
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```

### `**React.lazy**`

Function lets you render a dynamic import as a regular component.

```JavaScript
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </div>
  );
}
```

`React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.

> [!important] The lazy component should then be rendered inside a 
> 
> `Suspense` component, which allows us to show some ==**fallback**== content

> [!info] lazy – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/lazy#suspense-for-code-splitting](https://react.dev/reference/react/lazy#suspense-for-code-splitting)  

  

In particular, it is sometimes better to show the “old” ==**UI**== while the new ==**UI**== is being prepared. We can use the new [[Built-in React Hooks]] API to make React do this

```JavaScript
import React, { Suspense } from 'react';
import Tabs from './Tabs';
import Glimmer from './Glimmer';

const Comments = React.lazy(() => import('./Comments'));
const Photos = React.lazy(() => import('./Photos'));

function MyComponent() {
  const [tab, setTab] = React.useState('photos');
  
function handleTabSelect(tab) {
  startTransition(() => {
    setTab(tab);
  });
}

  return (
    <div>
      <Tabs onTabSelect={handleTabSelect} />
      <Suspense fallback={<Glimmer />}>
        {tab === 'photos' ? <Photos /> : <Comments />}
      </Suspense>
    </div>
  );
}
```

  

### Error boundaries

If the other ==module fails to load== (for example, due to network failure), it will trigger an error.

```JavaScript
import React, { Suspense } from 'react';
import MyErrorBoundary from './MyErrorBoundary';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

const MyComponent = () => (
  <div>
    <MyErrorBoundary>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </MyErrorBoundary>
  </div>
);
```

### **Route-based code splitting**

```JavaScript
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);
```

---

## Error Boundaries

Error boundaries are ==**React components**== that ==_**catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI**_== instead of the component tree that crashed. Error boundaries catch errors during ==rendering==, in ==lifecycle methods==, and in ==constructors of the whole tree below them==

> [!info] Component – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary)  

  

> [!important] ==**Error Boundaries**==
> 
> works based on a lifecycles method `componentDidCatch()`

> [!important] There are
> 
> ==**no**== Hook equivalents to the uncommon  `getSnapshotBeforeUpdate`, `getDerivedStateFromError` and `componentDidCatch`lifecycles yet, but ==**React**== plan to add them soon.

  

---

## High-Order Components (HOCs)

> [!info] Higher-Order Components – React  
> A JavaScript library for building user interfaces  
> [https://legacy.reactjs.org/docs/higher-order-components.html](https://legacy.reactjs.org/docs/higher-order-components.html)  

  

**==HOC==** ==is just a pattern== (input: Component & output: anotherComponent), the principals of **==HOC==** hide a compose of props in a _blackbox_ and reuse it.

> [!important] ==**HOC**==
> 
> can be replace logistically by ==CustomHooks==. However it’s depend on developers

  

---

## Performance optimization

==**React**== normally re-renders a component whenever its parent re-renders.

  

With `memo`, we can create a component that ==**React**== will ==not re-render== when its parent re-renders so long as its new props are the same as the old props

```JavaScript
import { memo, useState } from 'react';

export default function MyApp() {
  const [name, setName] = useState('');
  const [address, setAddress] = useState('');
  return (
    <>
      <label>
        Name{': '}
        <input value={name} onChange={e => setName(e.target.value)} />
      </label>
      <label>
        Address{': '}
        <input value={address} onChange={e => setAddress(e.target.value)} />
      </label>
      <Greeting name={name} />
    </>
  );
}

const Greeting = memo(function Greeting({ name }) {
  console.log("Greeting was rendered at", new Date().toLocaleTimeString());
  return <h3>Hello{name && ', '}{name}!</h3>;
});
```

  

> [!important] **Only rely on**
> 
> `**memo**` **as a** ==**performance optimization**  
>   
>   
> ==Optimizing with `memo` is only valuable when your component re-renders often with the same exact props, and its re-rendering logic is expensive.  
>   
> If there is no perceptible lag when your component re-renders,  
> `memo` is ==unnecessary==.

### `<Profiler>`

`<Profiler>` lets us measure rendering performance of a React tree programmatically.

> [!info] Profiler – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react/Profiler](https://react.dev/reference/react/Profiler)  

  

---

## React DOM built-in components

### Common components

> [!info] Common components (e.g. div) – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react-dom/components/common](https://react.dev/reference/react-dom/components/common)  

### **Form components**

> [!info] React DOM Components – React  
> The library for web and native user interfaces  
> [https://react.dev/reference/react-dom/components](https://react.dev/reference/react-dom/components)  

- `<input>`
- `<option>`
- `<progress>`
- `<select>`
- `<textarea>`

  

---

## Testing

There are 2 main ways to test ==**React**== components

- ==**Rendering component trees:**== a simplified test environment and asserting on their output
- **==Running a complete app:==** a realistic environment (aka _end-to-end_ test)

### Recommended Tools

- Jest
    
    > [!info] Jest  
    > Jest is a delightful JavaScript Testing Framework with a focus on simplicity.  
    > [https://jestjs.io/](https://jestjs.io/)  
    
- React Testing Library
    
    > [!info] React Testing Library | Testing Library  
    > React Testing Library builds on top of DOM Testing Library by adding  
    > [https://testing-library.com/react](https://testing-library.com/react)  
    

  

> [!important] There is an easy way to setup testing environment for
> 
> ==**React**==.  
> It’s  
> `==**Vitest**==`

  

> [!info] Vitest  
> Next generation testing framework powered by Vite  
> [https://vitest.dev/](https://vitest.dev/)  

```Bash
pnpm install -D vitest@latest
```

  

After install `vitest`, we need to setup the configuration for it.

```JSON
"compilerOptions" : {
	...,
	"types": ["vitest/globals"],
}
```

```TypeScript
/// <reference types="vitest" />
/// <reference types="vite/client" />

import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react-swc'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './src/test/setup.ts',
    css: true,
  },
})
```

```TypeScript
import '@testing-library/jest-dom'
```