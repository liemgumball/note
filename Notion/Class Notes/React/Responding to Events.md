Handling events with **React** elements is very similar to handling events on **DOM** elements. There are some syntax differences:

- React events are named using camelCase, rather than lowercase.
- With JSX you pass a function as the event handler, rather than a string.

**React** lets you add *event handlers* to your JSX. Event handlers are your own functions that will be triggered in response to interactions like clicking, hovering, focusing form inputs, and so on.

## **Event propagation**

<aside>
💡 Event handlers will also catch events from any children your component might have

</aside>

```jsx
<div className="Toolbar" onClick={() => {
      alert('You clicked on the toolbar!');
    }}>
      <button onClick={() => alert('Playing!')}>
        Play Movie
      </button>
</div>

// onclick => Playing! => You clicked on the toolbar!
```

We say that an event “*bubbles*” or “*propagates*” up the tree: it starts with where the event happened, and then goes up the tree.

### **Stopping propagation**

If you want to prevent an event from reaching parent components, you need to call `e.stopPropagation()` like this `Button` component does:

```jsx
<button onClick={e => {
   e.stopPropagation();
   onClick();
}}>
   {children}
</button>
```

### **Preventing default behavior**

Some browser events have default behavior associated with them. For example, a `<form>` submit event, which happens when a button inside of it is clicked, will reload the whole page by default

```jsx
<form onSubmit={() => alert('Submitting!')}>
  <input />
	<button>Send</button>
</form>
```