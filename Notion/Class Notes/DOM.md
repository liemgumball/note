Created: July 10, 2023 9:00 AM
Class: Agility IO InternShip
Type: Front-end
Materials: https://www.digitalocean.com/community/tutorials/how-to-modify-attributes-classes-and-styles-in-the-dom, https://www.digitalocean.com/community/tutorials/understanding-events-in-javascript
Reviewed: Yes
Edited: May 10, 2025 2:46 PM

# **HTML DOM (Document Object Model)**

## The **HTML DOM** model is constructed as a tree of **Objects**

![Untitled](Notion/Class%20Notes/DOM/Untitled.png)

## With the object model, JavaScript gets all the power it needs to create dynamic HTML:

- JavaScript can change all the HTML elements in the page
- JavaScript can change all the HTML attributes in the page
- JavaScript can change all the CSS styles in the page
- JavaScript can remove existing HTML elements and attributes
- JavaScript can add new HTML elements and attributes
- JavaScript can react to all existing HTML events in the page
- JavaScript can create new HTML events in the page

### **The DOM Programming Interface**

<aside>
💡 In the DOM, all HTML elements are defined as **objects**.

</aside>

- A **property** is a value that you can get or set (like changing the content of an HTML element).
- A **method** is an action you can do (like add or deleting an HTML element).

```html
<html>
<body>

	<p id="demo"></p>
	
	<script>
		document.getElementById("demo").innerHTML = "Hello World!";
	</script>

</body>
</html>
```

In the example above:

- The `getElementById` is **method**
- The `innerHTML` is **property**

## DOM Elements

- Finding HTML elements by id

```jsx
const element = document.getElementById("intro");
```

- Finding HTML elements by tag name

```jsx
const element = document.getElementsByTagName("p");
```

- Finding HTML elements by class name

```jsx
const x = document.getElementsByClassName("intro");
```

- Finding HTML elements by CSS selectors

```jsx
const x = document.querySelectorAll("p.intro");
```

- Finding HTML elements by HTML object collections
    - `document.anchors`
    - `document.body`
    - `document.documentElement`
    - `document.embeds`
    - `document.forms`
    - `document.head`
    - `document.images`
    - `document.links`
    - `document.scripts`
    - `document.title`

```jsx
const x = document.forms["frm1"];
let text = "";
for (let i = 0; i < x.length; i++) {
  text += x.elements[i].value + "<br>";
}
document.getElementById("demo").innerHTML = text;
```

## **JavaScript HTML DOM**

<aside>
💡 The HTML DOM allows JavaScript to change the content of HTML elements.

</aside>

### **Changing HTML Content**

The easiest way to modify the content of an HTML element is by using the `innerHTML` property

```html
<!DOCTYPE html>
<html>
<body>

	<h1 id="id01">Old Heading</h1>
	
	<script>
		const element = document.getElementById("id01");
		element.innerHTML = "New Heading";
</script>

</body>
</html>
```

### **Changing the Value of an Attribute**

```html
<!DOCTYPE html>
<html>
<body>

	<img id="myImage" src="smiley.gif">
	
	<script>
		document.getElementById("myImage").src = "landscape.jpg";
	</script>

</body>
</html>
```

### **Dynamic HTML content**

JavaScript can create dynamic HTML content:

```html
<!DOCTYPE html>
<html>
<body>

	<script>
		document.getElementById("demo").innerHTML = "Date : " + Date(); 
	</script>

</body>
</html>
```

### `document.write()` (shouldn’t use)

In JavaScript, `document.write()` can be used to write directly to the HTML output stream:

```html
<!DOCTYPE html>
<html>
<body>

	<p>Bla bla bla</p>
	
	<script>
		document.write(Date());
	</script>
	
	<p>Bla bla bla</p>

</body>
</html>
```

<aside>
💡 Never use `document.write()` after the document is loaded. It will overwrite the document.

</aside>

## **JavaScript Forms**

### JavaScript is often used to validate

Data validation is the process of ensuring that user input is clean, correct, and useful.

```html
<head>	
	<script>
		function validateForm() {
		  let x = document.forms["myForm"]["fname"].value;
		  if (x == "") {
		    alert("Name must be filled out");
		    return false;
		  }
		}
	</script>
</head>
<body>

	<h2>JavaScript Validation</h2>
	
	<form name="myForm" action="/action_page.php" 
	onsubmit="return validateForm()" method="post">
	  Name: <input type="text" name="fname">
	  <input type="submit" value="Submit">
	</form>
</body>
```

## **JavaScript HTML DOM Events**

HTML DOM allows JavaScript to react to HTML **events**:

- When a user clicks the mouse
- When a web page has loaded
- When an image has been loaded
- When the mouse moves over an element
- When an input field is changed
- When an HTML form is submitted
- When a user strokes a key

```html
<!DOCTYPE html>
<html>
	<body>
	
	<h1 onclick="changeText(this)">Click on this text!</h1>
	
	<script>
		function changeText(id) {
		  id.innerHTML = "Ooops!";
		}
	</script>
	
	</body>
</html>
```

### DOM Events

| Event | Occurs When | Belongs To |
| --- | --- | --- |
| `abort` | The loading of a media is aborted | UiEvent, Event |
| `afterprint` | A page has started printing | Event |
| `animationend` | A CSS animation has completed | AnimationEvent |
| `animationiteration` | A CSS animation is repeated | AnimationEvent |
| `animationstart` | A CSS animation has started | AnimationEvent |
| `beforeprint` | A page is about to be printed | Event |
| `beforeunload` | Before a document is about to be unloaded | UiEvent, Event |
| `blur` | An element loses focus | FocusEvent |
| `canplay` | The browser can start playing a media (has buffered enough to begin) | Event |
| `canplaythrough` | The browser can play through a media without stopping for buffering | Event |
| `change` | The content of a form element has changed | Event |
| `click` | An element is clicked on | MouseEvent |
| `contextmenu` | An element is right-clicked to open a context menu | MouseEvent |
| `copy` | The content of an element is copied | ClipboardEvent |
| `cut` | The content of an element is cutted | ClipboardEvent |
| `dblclick` | An element is double-clicked | MouseEvent |
| `drag` | An element is being dragged | DragEvent |
| `dragend` | Dragging of an element has ended | DragEvent |
| `dragenter` | A dragged element enters the drop target | DragEvent |
| `dragleave` | A dragged element leaves the drop target | DragEvent |
| `dragover` | A dragged element is over the drop target | DragEvent |
| `dragstart` | Dragging of an element has started | DragEvent |
| `drop` | A dragged element is dropped on the target | DragEvent |
| `durationchange` | The duration of a media is changed | Event |
| `ended` | A media has reach the end ("thanks for listening") | Event |
| `error` | An error has occurred while loading a file | ProgressEvent, UiEvent, Event |
| `focus` | An element gets focus | FocusEvent |
| `focusin` | An element is about to get focus | FocusEvent |
| `focusout` | An element is about to lose focus | FocusEvent |
| `fullscreenchange` | An element is displayed in fullscreen mode | Event |
| `fullscreenerror` | An element can not be displayed in fullscreen mode | Event |
| `hashchange` | There has been changes to the anchor part of a URL | HashChangeEvent |
| `input` | An element gets user input | InputEvent, Event |
| `invalid` | An element is invalid | Event |
| `keydown` | A key is down | KeyboardEvent |
| `keypress` | A key is pressed | KeyboardEvent |
| `keyup` | A key is released | KeyboardEvent |
| `load` | An object has loaded | UiEvent, Event |
| `loadeddata` | Media data is loaded | Event |
| `loadedmetadata` | Meta data (like dimensions and duration) are loaded | Event |
| `loadstart` | The browser starts looking for the specified media | ProgressEvent |
| `message` | A message is received through the event source | Event |
| `mousedown` | The mouse button is pressed over an element | MouseEvent |
| `mouseenter` | The pointer is moved onto an element | MouseEvent |
| `mouseleave` | The pointer is moved out of an element | MouseEvent |
| `mousemove` | The pointer is moved over an element | MouseEvent |
| `mouseover` | The pointer is moved onto an element | MouseEvent |
| `mouseout` | The pointer is moved out of an element | MouseEvent |
| `mouseup` | A user releases a mouse button over an element | MouseEvent |
| `mousewheel` | Deprecated. Use the wheel event instead | WheelEvent |
| `offline` | The browser starts working offline | Event |
| `online` | The browser starts working online | Event |
| `open` | A connection with the event source is opened | Event |
| `pagehide` | User navigates away from a webpage | PageTransitionEvent |
| `pageshow` | User navigates to a webpage | PageTransitionEvent |
| `paste` | Some content is pasted in an element | ClipboardEvent |
| `pause` | A media is paused | Event |
| `play` | The media has started or is no longer paused | Event |
| `playing` | The media is playing after beeing paused or buffered | Event |
| `popstate` | The window's history changes | PopStateEvent |
| `progress` | The browser is downloading media data | Event |
| `ratechange` | The playing speed of a media is changed | Event |
| `resize` | The document view is resized | UiEvent, Event |
| `reset` | A form is reset | Event |
| `scroll` | An scrollbar is being scrolled | UiEvent, Event |
| `search` | Something is written in a search field | Event |
| `seeked` | Skipping to a media position is finished | Event |
| `seeking` | Skipping to a media position is started | Event |
| `select` | User selects some text | UiEvent, Event |
| `show` | A <menu> element is shown as a context menu | Event |
| `stalled` | The browser is trying to get unavailable media data | Event |
| `storage` | A Web Storage area is updated | StorageEvent |
| `submit` | A form is submitted | Event |
| `suspend` | The browser is intentionally not getting media data | Event |
| `timeupdate` | The playing position has changed (the user moves to a different point in the media) | Event |
| `toggle` | The user opens or closes the <details> element | Event |
| `touchcancel` | The touch is interrupted | TouchEvent |
| `touchend` | A finger is removed from a touch screen | TouchEvent |
| `touchmove` | A finger is dragged across the screen | TouchEvent |
| `touchstart` | A finger is placed on a touch screen | TouchEvent |
| `transitionend` | A CSS transition has completed | TransitionEvent |
| `unload` | A page has unloaded | UiEvent, Event |
| `volumechange` | The volume of a media is changed (includes muting) | Event |
| `waiting` | A media is paused but is expected to resume (e.g. buffering) | Event |
| `wheel` | The mouse wheel rolls up or down over an element | WheelEvent |

## **JavaScript HTML DOM EventListener**

**The `addEventListener()` method**

```html
<h2>JavaScript addEventListener()</h2>

<p>This example uses the addEventListener()
 method to attach a click event to a button.</p>

<button id="myBtn">Try it</button>

<p id="demo"></p>

<script>
	document.getElementById("myBtn").addEventListener("click", displayDate);
	
	function displayDate() {
	  document.getElementById("demo").innerHTML = Date();
	}
</script>
```

### Syntax

```jsx
element.addEventListener(event, function, useCapture);
```

<aside>
💡 We can add many events to the same element, without overwriting existing events, add events of different types to the same element

</aside>

### **Add an Event Handler to the window Object**

```html
<h2>JavaScript addEventListener()</h2>

<p>This example uses the addEventListener() method on the window object.</p>

<p>Try resizing this browser window to trigger the "resize" event handler.</p>

<p id="demo"></p>

<script>
window.addEventListener("resize", function(){
  document.getElementById("demo").innerHTML = Math.random();
});
</script>
```

### **Event Bubbling or Event Capturing?**

Event propagation is a way of defining the element order when an event occurs. If you have a `<p>` element inside a `<div>` element, and the user clicks on the `<p>` element, which element's "`click`" event should be handled first?

- In *bubbling* the inner most element's event is handled first and then the outer: the `<p>` element's click event is handled first, then the `<div>` element's click event.
- In *capturing* the outer most element's event is handled first and then the inner: the `<div>` element's click event will be handled first, then the `<p>` element's click event.

```jsx
element.addEventListener(event, function, useCapture);
//true or false
document.getElementById("myP").addEventListener("click", myFunction, true);
document.getElementById("myDiv").addEventListener("click", myFunction, true);
```

## **JavaScript HTML DOM Navigation**

<aside>
💡 With the HTML DOM, you can navigate the node tree using node relationships.

</aside>

![Untitled](Notion/Class%20Notes/DOM/Untitled%201.png)

### Example

```jsx
<html>

  <head>
    <title>DOM Tutorial</title>
  </head>

  <body>
    <h1>DOM Lesson one</h1>
    <p>Hello world!</p>
  </body>

</html>
```

From the HTML above we can read:

- `<html>` is the root node
- `<html>` has no parents
- `<html>` is the parent of `<head>` and `<body>`
- `<head>` is the first child of `<html>`
- `<body>` is the last child of `<html>`

and:

- `<head>` has one child: `<title>`
- `<title>` has one child (a text node): "DOM Tutorial"
- `<body>` has two children: `<h1>` and `<p>`
- `<h1>` has one child: "DOM Lesson one"
- `<p>` has one child: "Hello world!"
- `<h1>` and `<p>` are siblings

### Navigate between nodes

- `parentNode`
- `childNodes[*nodenumber*]`
- `firstChild`
- `lastChild`
- `nextSibling`
- `previousSibling`

### **Child Nodes and Node Values**

The value of the text node can be accessed by the node's `innerHTML` property

```jsx
myTitle = document.getElementById("demo").innerHTML;
```

or

```jsx
myTitle = document.getElementById("demo").firstChild.nodeValue;
```

or

```jsx
myTitle = document.getElementById("demo").childNodes[0].nodeValue;
```

```jsx
<body>

<h1 id="id01">My Page</h1>
<p id="id02"></p>

<script>
	document.getElementById("id02").innerHTML = document.getElementById("id01").innerHTML;
</script>

</body>
```

### **The `nodeName` Property**

- nodeName is read-only
- nodeName of an element node is the same as the tag name
- nodeName of an attribute node is the attribute name
- nodeName of a text node is always #text
- nodeName of the document node is always #document

```html
<h1 id="id01">My First Page</h1>
<p id="id02"></p> //H1

<script>
document.getElementById("id02").innerHTML = document.getElementById("id01").nodeName;
</script>
```

### **The `nodeValue` Property**

- nodeValue for element nodes is `null`
- nodeValue for text nodes is the text itself
- nodeValue for attribute nodes is the attribute value

### **The `nodeType` Property**

The `nodeType` property is read only. It returns the type of a node.

```html
<h1 id="id01">My First Page</h1>
<p id="id02"></p> //1

<script>
document.getElementById("id02").innerHTML = document.getElementById("id01").nodeType;
</script>
```

## **JavaScript HTML DOM Elements (Nodes)**

### **Creating New HTML Elements (Nodes)**

```html
<div id="div1">
	<p id="p1">This is a paragraph.</p>
	<p id="p2">This is another paragraph.</p>
</div>

<script>
	const para = document.createElement("p");
	const node = document.createTextNode("This is new.");
	para.appendChild(node);

	//insert after
	const element = document.getElementById("div1");
	element.appendChild(para);
	//insert before
	const child = document.getElementById("p1");
	element.insertBefore(para, child);
</script>
```

### **Removing Existing HTML Elements**

To remove an HTML element, use the `remove()` method:

```html
<div>
  <p id="p1">This is a paragraph.</p>
  <p id="p2">This is another paragraph.</p>
</div>

<script>
	const elmnt = document.getElementById("p1"); elmnt.remove();
</script>
```

### **Removing a Child Node**

To remove an HTML element, use the `removeChild()` method:

```html
<div id="div1">
  <p id="p1">This is a paragraph.</p>
  <p id="p2">This is another paragraph.</p>
</div>

<script>
	const parent = document.getElementById("div1");
	const child = document.getElementById("p1");
	parent.removeChild(child);
</script>
```

### **Replacing HTML Elements**

To replace an element to the HTML DOM, use the `replaceChild()` method:

```html
<div id="div1">
  <p id="p1">This is a paragraph.</p>
  <p id="p2">This is another paragraph.</p>
</div>

<script>
	const para = document.createElement("p");
	const node = document.createTextNode("This is new.");
	para.appendChild(node);
	
	const parent = document.getElementById("div1");
	const child = document.getElementById("p1");
	parent.replaceChild(para, child);
</script>
```

## **JavaScript HTML DOM Collections**

The `getElementsByTagName()` method returns an `HTMLCollection` object.

```html
<h2>JavaScript HTML DOM</h2>

<p>Hello World!</p>

<p>Hello Norway!</p>

<p id="demo"></p>

<script>
	const myCollection = document.getElementsByTagName("p");
	
	document.getElementById("demo").innerHTML = myCollection[1].innerHTML 
																							+ myCollection.length;
	//Hello Norway! 3
</script>
```

<aside>
💡 **An HTMLCollection is NOT an array!**

An HTMLCollection may look like an array, but it is not.

You can loop through the list and refer to the elements with a number (just like an array).

However, you cannot use array methods like `valueOf()`, `pop()`, `push()`, or `join()` on an HTMLCollection.

</aside>

## **JavaScript HTML DOM Node Lists**

A `NodeList` object is a list (collection) of nodes extracted from a document.

A `NodeList` object is almost the same as an `HTMLCollection` object.

Most browsers return a NodeList object for the method `querySelectorAll()`.

```html
<h2>JavaScript HTML DOM</h2>

<p>Hello World!</p>

<p>Hello Norway!</p>

<p id="demo"></p>

<script>
	const myNodelist = document.querySelectorAll("p");
	
	document.getElementById("demo").innerHTML = myNodelist[1].innerHTML
																							+ myNodeList.length;
//Hello Norway!3

</script>
```

<aside>
💡 Not an Array!

A NodeList may look like an array, but it is not.

You can loop through a NodeList and refer to its nodes by index.

But, you cannot use Array methods like `push()`, `pop()`, or `join()` on a NodeList.

</aside>

## Modifying Attributes

In JavaScript, we have four methods for modifying element attributes:

| Method | Description | Example |
| --- | --- | --- |
| `hasAttribute()` | Returns a true or false boolean | element.hasAttribute('href'); |
| `getAttribute()` | Returns the value of a specified attribute or null | element.getAttribute('href'); |
| `setAttribute()` | Adds or updates value of a specified attribute | element.setAttribute('href', 'index.html'); |
| `removeAttribute()` | Removes an attribute from an element | element.removeAttribute('href'); |

```html
<body>

	<img src="https://js-tutorials.nyc3.digitaloceanspaces.com/shark.png">
	<script>
		// Assign image element
		const img = document.querySelector('img');
		
		img.hasAttribute('src');                // returns true
		img.getAttribute('src');                // returns "...shark.png"
		img.removeAttribute('src');             // remove the src attribute and value
	</script>

</body>
```

## Modifying Classes

| Method/Property | Description | Example |
| --- | --- | --- |
| `className` | Gets or sets class value | element.className; |
| `classList.add()` | Adds one or more class values | element.classList.add('active'); |
| `classList.toggle()` | Toggles a class on or off | element.classList.toggle('active'); |
| `classList.contains()` | Checks if class value exists | element.classList.contains('active'); |
| `classList.replace()` | Replace an existing class value with a new class value | element.classList.replace('old', 'new'); |
| `classList.remove()` | Remove a class value | element.classList.remove('active'); |

```html
<body>

	<div>Div 1</div>
	<div class="active">Div 2</div>

		<script>
			// Select the second div by class name
			const activeDiv = document.querySelector('.active');
			
			activeDiv.classList.add('hidden');                
			// Add the hidden class
			activeDiv.classList.remove('hidden');             
			// Remove the hidden class
			activeDiv.classList.toggle('hidden');             
			// Switch between hidden true and false
			activeDiv.classList.replace('active', 'warning'); 
			// Replace active class with warning class
	</script>
</body>
```

## Modiying Styles

```jsx
// Select div
const div = document.querySelector('div');

// Apply style to div
div.setAttribute('style', 'text-align: center');
```

This will remove all existing inline styles from the element. 

Since this is likely not the intended effect, it is better to use the `style` attribute directly

```jsx
div.style.height = '100px';
div.style.width = '100px';
div.style.border = '2px solid black';
```