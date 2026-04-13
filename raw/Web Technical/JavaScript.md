---
Created: 2023-07-07T09:35
Class: Agility IO InternShip
Type: Front-end
Materials:
  - https://drive.google.com/file/d/1GUC9vvKTX0jOoPQ93wzrE5Z7a4BXVu9j/view
Reviewed: true
Edited: 2025-05-10T14:45
---
https://github.com/liemgumball/javascript-training

## **Syntax**

- White space
- Case sensitiv
- Literals
- Identifiers
- Comments

## **Variable**

- `var`
- `const`
- `let`

## **Types**

- Primitive Types
    - number
    - string
    - boolean
    - symbol
- Object Types

## Operators

> [!important] **Note**
> 
> that we also have `==` and `!=` in JavaScript, but I highly suggest to only use `===` and `!==` because they can prevent some subtle problems.

|Operator|Name|Description|
|---|---|---|
|`&`|AND|Sets each bit to 1 if both bits are 1|
|`\|`|OR|Sets each bit to 1 if one of two bits is 1|
|`^`|XOR|Sets each bit to 1 if only one of two bits is 1|
|`~`|NOT|Inverts all the bits|
|`<<`|Zero fill left shift|Shifts left by pushing zeros in from the right and let the leftmost bits fall off|
|`>>`|Signed right shift|Shifts right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off|
|`>>>`|Zero fill right shift|Shifts right by pushing zeros in from the left, and let the rightmost bits fall off|

- `yeild` : operator is used to pause and resume a **==[generator function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)====.==**

```JavaScript
function* anotherGenerator(i) {
  yield i + 1;
  yield i + 2;
  yield i + 3;
}

function* generator(i) {
  yield i;
  yield* anotherGenerator(i);
  yield i + 10;
}

const gen = generator(10);

console.log(gen.next().value); // 10
console.log(gen.next().value); // 11
console.log(gen.next().value); // 12
console.log(gen.next().value); // 13
console.log(gen.next().value); // 20
```

## String

- `string.length`
- `string.slice()`: extracts a part of a string and returns the extracted part in a new string.
- `string.substring()`: similar to `slice()` but: the start and end values less than 0 are treated as 0
- `string.substr()`: similar to `slice()`, the difference is that the second parameter specifies the **length** of the extracted part.
- `string.replace()`:
    
    ```JavaScript
    let text = "Please visit Microsoft!";
    let newText = text.replace("Microsoft", "AgilityIO");
    //By default, the replace() method is case sensitive.
    // Writing MICROSOFT (with upper-case) will not work
    ```
    
    To replace case insensitive, use a **regular expression** with an `/i` flag (insensitive):
    
    ```JavaScript
    let text = "Please visit Microsoft!";
    let newText = text.replace(/MICROSOFT/i, "AgilityIO");
    ```
    
- `string.replaceAll()`: allows you to specify a regular expression instead of a string to be replaced.
- `string.toUperCase()`
- `string.toLowerCase()`
- `string.concat()`: joins two or more strings
- `string.trim()`: removes ==whitespace== from both sides of a string
- `string.trimStart()`
- `string.trimEnd()`
- `string.padStart()`: It pads a string with another string (multiple times) until it reaches a given length.

```JavaScript
let numb = 5;
let text = numb.toString();
let padded = text.padStart(4,"x");
//xxx5
```

- `string.padEnd()`
- `string.chartAt()`: returns the character at a specified ==index== (position) in a string
- `string.chartCodeAt()`: returns a ==UTF-16== code (an integer between 0 and 65535)
- `string.split()`: convert a string to an array

## String search methods

- String `indexOf()`: returns the ==**index**== (position) the ==**first**== occurrence of a string in a string

```JavaScript
let text = "Please locate where 'locate' occurs!";
let index = text.indexOf("locate");
//7
```

- String `lastIndexOf()`: returns the ==**index**== of the ==**last**== occurrence of a specified text in a string

```JavaScript
let text = "Please locate where 'locate' occurs!";
let index = text.lastIndexOf("locate");
//21
```

> [!important] Both 
> 
> `indexOf()`, and `lastIndexOf()` return -1 if the text is not found. Both methods accept a ==second parameter== as the ==starting position== for the search

```JavaScript
let text = "Please locate where 'locate' occurs!";
let index = text.indexOf("locate", 15);
//21
```

- String `search()`: searches a string for a string (or a regular expression) and ==returns== the ==position== of the match

```JavaScript
let text = "Please locate where 'locate' occurs!";
text.search("locate");

let text = "Please locate where 'locate' occurs!";
text.search(/locate/);
```

> [!important] The two methods are 
> 
> ==**NOT**== equal. These are the differences:
> 
> - The `search()` method cannot take a second start position argument.
> - The `indexOf()` method cannot take powerful search values (regular expressions).

- String `match()`: returns an array containing the results of matching a string against a string (or a regular expression).

```JavaScript
let text = "The rain in SPAIN stays mainly in the plain";
const Arr = text.match(/ain/gi);

//Arr = [ain, AIN, ain, ain]
```

- String `matchAll()`
- String `includes()`: returns true if a string contains a specified value
- String `startsWith()`: returns `true` if a string begins with a specified value

```JavaScript
let text = "Hello world, welcome to the universe.";
text.startsWith("Hello");
//true
```

- String `endsWith()`

  

## ==String template==

```JavaScript
let firstName = "John";
let lastName = "Doe";

let text = `Welcome ${firstName}, ${lastName}!`;

let price = 10;
let VAT = 0.25;

let total = `Total: ${(price * (1 + VAT)).toFixed(2)}`;
```

## Numbers

> [!important] JavaScript has only one type of number. Numbers can be written with or without
> 
> ==decimals==.

- `toString()`
- `toExponential()`: returns a string, with a number rounded and written using ==exponential notation==.
- `toFixed()`: returns a string, with the number written with a specified number of decimals.
- `toPrecision()`: returns a string, with a number written with a specified length.
- `ValueOf()`: returns a number as a number

```JavaScript
let x = 123;
x.valueOf(); //123
(123).valueOf(); //123
(100 + 23).valueOf(); //123
```

## Array

We can initialize an empty array in these 2 different ways:

```JavaScript
const a = []
const a = Array()
```

### Array properties

- `Array[Symbol.species]`: static accessor property returns the constructor used to construct return values from array methods.

> [!important] The
> 
> ==returned constructor== will be used to ==construct== the return value of the array method. This makes it technically possible to make array methods ==return objects unrelated to arrays==.

- `Array.prototype[@@unscopables]` : an empty object only containing property names with the value `true` for the ==statement-binding== purpose
- `Array.length`

### Add an item to array

- add at end of array `a.push(4)`
- add at begin of array `a.unshift(4)`

### Remove an item from array

- `a.pop()`
- `a.shift()`

### Join two or more array

- You can join multiple arrays by using `concat()` :
    
    ```JavaScript
    const a = [1, 2]
    const b = [3, 4]
    const c = a.concat(b) //[1,2,3,4]
    a //[1,2]
    b //[3,4]
    ```
    
- You can also use the spread operator `( ... )` in this way:
    
    ```JavaScript
    const a = [1, 2]
    const b = [3, 4]
    const c = [...a, ...b]
    c //[1,2,3,4]
    ```
    

### Find a specific item in the array

- You can use the `find()` method of an array:
    
    ```JavaScript
    a.find((element, index, array) => {
    //return true or false
    })
    ```
    
    A commonly used syntax is:
    
    ```JavaScript
    a.find(x => x.id === my_id)
    ```
    
- `findIndex()` works similarly to `find()` , but returns the index of the first item that returns `true`, and if not found, it returns `undefined` :
    
    ```JavaScript
    a.findIndex((element, index, array) => {
    //return true or false
    })
    ```
    
- Another method is `includes()` :
    
    Returns true if `a` contains `value` .
    
    ```JavaScript
    a.includes(value)
    ```
    
    Returns true if `a` contains `value` after the position `i`
    
    ```JavaScript
    a.includes(value, i)
    ```
    
    ### Array Methods
    
    - `length`
    - `toString()` 
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Apple", "Mango"];
        document.getElementById("demo").innerHTML = fruits.toString();
        //Banana,Orange,Apple,Mango
        ```
        
    - `push()`
    - `pop()`
    - `shift()`
    - `unshift()`
    - `join()`
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Apple", "Mango"];
        document.getElementById("demo").innerHTML = fruits.join(" * ");
        //Banana * Orange * Apple * Mango
        ```
        
    - **Changing Elements**
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Apple", "Mango"];
        fruits[0] = "Kiwi";
        //Kiwi,Orange,Apple,Mango
        ```
        
    - `delete()`: Using `delete` leaves `undefined` ==holes== in the array
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Apple", "Mango"];
        
        document.getElementById("demo1").innerHTML =
        "The first fruit is: " + fruits[0]; //Banana
        
        delete fruits[0];
        
        document.getElementById("demo2").innerHTML =
        "The first fruit is: " + fruits[0]; //undefine
        ```
        
    - `concat()`: creates a new array by ==merging== (concatenating) existing arrays
        
        ```JavaScript
        const myGirls = ["Cecilie", "Lone"];
        const myBoys = ["Emil", "Tobias", "Linus"];
        
        const myChildren = myGirls.concat(myBoys);
        //Cecilie,Lone,Emil,Tobias,Linus
        ```
        
    - `flat()`: ==Flattening== an array is the process of ==reducing== the ==dimensionality== of an array. The `flat()` method creates a new array with sub-array elements concatenated to a specified depth.
        
        ```JavaScript
        const myArr = [[1,2],[3,4],[5,6]];
        const newArr = myArr.flat();
        //[1,2,3,4,5,6]
        ```
        
    - `splice()`: adds new items to an array
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Apple", "Mango"];
        let removed = fruits.splice(2, 2, "Lemon", "Kiwi"); //Apple, Mango
        //Banana,Orange,Lemon,Kiwi
        ```
        
        The first parameter (2) defines the position ==**where**== new elements should be ==**added**== (spliced in).
        
        The second parameter (0) defines ==**how many**== elements should be ==**removed**==.
        
        The rest of the parameters ("Lemon" , "Kiwi") define the **==new elements==** to be ==**added**==.
        
    - `slice()`: slices out a piece of an array into a new array.
        
        ```JavaScript
        const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
        console.log(fruits);
        //Banana,Orange,Lemon,Apple,Mango
        
        const citrus = fruits.slice(1, 3);
        console.log(citrus);
        //Orange,Lemon
        ```
        
        > [!important] The 
        > 
        > `slice()` method creates a new array.
        > 
        > The `slice()` method does not remove any elements from the source array.
        
    
      
    
    - `sort()`
        
        > [!important] By default, the 
        > 
        > `sort()` function sorts values as **strings**.
        
        This works well for strings ("Apple" comes before "Banana").
        
        However, if numbers are sorted as strings, =="25"== is bigger than =="100"==, because =="2"== is bigger than =="1"==.
        
        The `sort()` method will produce incorrect result when sorting numbers.
        
        You can fix this by providing a ==**compare function**==:
        
        ```JavaScript
        const points = [40, 100, 1, 5, 25, 10];
        points.sort(function(a, b){return a - b}); //ascending order
        ```
        
    - `reverse()`
    - `fill(value, start, end)`
    - `filter(callbackFn, thisArg)`
        
        ```JavaScript
        const words = ['spray', 'limit', 'elite', 
        'exuberant', 'destruction', 'present'];
        
        const result = words.filter(word => word.length > 6);
        
        console.log(result);
        // Expected output: Array ["exuberant", "destruction", "present"]
        ```
        
    - `reduce(callbackFn, intialValue)`
        - The `callbackFn` includes `(accumulator, currentValue, index, array) = {}`
    - **Using** `**Math.max()**` **on an Array**
        
        ```JavaScript
        function myArrayMax(arr) {
          return Math.max.apply(null, arr);
        }
        ```
        

## Iteration methods

- `while`
    
    ```JavaScript
    while (true) {
    	if (somethingIsTrue) break
    
    	if (somethingIsTrue) continue
    	//do something else
    }
    ```
    
- `for`
    
    ```JavaScript
    const list = ['a', 'b', 'c']
    for (let i = 0; i < list.length; i++) {
    	console.log(list[i]) //value
    	console.log(i) //index
    }
    ```
    
- `for ... in`: loops through the properties of an **Object**
    
    ```JavaScript
    const person = {fname:"John", lname:"Doe", age:25};
    
    let text = "";
    for (let x in person) {
      text += person[x];
    }
    //John Doe 25
    ```
    
- `for ... of`: loop over iterable data structures such as Arrays, Strings, Maps, NodeLists, and more:
    
    ```JavaScript
    const list = ['a', 'b', 'c']
    for (const value of list) {
    	console.log(value) //value
    }
    ```
    
- `forEach((currentValue, index, array) => {})`: executes a provided function once for each array element.
    
    ```JavaScript
    const array = [1, 2, 3];
    
    array.forEach((currentValue, index, array) => {
      console.log(`Value: ${currentValue}, Index: ${index}, Array: ${array}`);
    });
    ```
    
- `every((currentValue, index, array) => {})`: call every element in the array until it either reaches the end or encounters an element for which the callback function returns `**false**`
    
    ```JavaScript
    const isBelowThreshold = (currentValue) => currentValue < 40;
    
    const array1 = [1, 30, 39, 29, 10, 13];
    
    console.log(array1.every(isBelowThreshold));
    // Expected output: true
    ```
    
- `map((currentValue, index, array) => {})`: **creates a new array** populated with the results of calling a provided function on every element in the calling array.
    
    ```JavaScript
    const array1 = [1, 4, 9, 16];
    
    // Pass a function to map
    const map1 = array1.map(x => x * 2);
    
    console.log(map1);
    // Expected output: Array [2, 8, 18, 32]
    ```
    
      
    

## Sets

> [!important] A JavaScript
> 
> **==Set==** is a collection of ==unique== values.
> 
> Each value can only occur **==once==** in a Set.

|Method|Description|
|---|---|
|`new Set()`|Creates a new Set|
|`add()`|Adds a new element to the Set|
|`delete()`|Removes an element from a Set|
|`has()`|Returns true if a value exists in the Set|
|`forEach()`|Invokes a callback for each element in the Set|
|`values()`|Returns an iterator with all the values in a Set|
|**Property**|**Description**|
|`size`|Returns the number of elements in a Set|

## Maps

> [!important] A Map holds
> 
> **==key-value==** pairs where the keys can be ==any datatype==.
> 
> A Map remembers the original insertion order of the keys.

|Method|Description|
|---|---|
|`new Map()`|Creates a new Map|
|`set()`|Sets the value for a key in a Map|
|`get()`|Gets the value for a key in a Map|
|`delete()`|Removes a Map element specified by the key|
|`has()`|Returns true if a key exists in a Map|
|`forEach()`|Calls a function for each key/value pair in a Map|
|`entries()`|Returns an iterator with the [key, value] pairs in a Map|
|**Property**|**Description**|
|`size`|Returns the number of elements in a Map|

## JavaScript Errors

- `try` defines a code block to run (to try)
- `catch` defines a code block to handle any **==error==**
- `finally` defines a code block to run regardless of the result
    
    ```JavaScript
    try {
      Block of code to try
    }
    catch(err) {
      Block of code to handle errors
    }
    finally {
      Block of code to be executed regardless of the result of the "try / catch"
    }
    ```
    
- `throw` defines a custom ==error==
    
    ```JavaScript
    let x = document.getElementById("demo").value;
      try { 
        if(x.trim() == "")  throw "empty";
        if(isNaN(x)) throw "not a number";
        x = Number(x);
        if(x < 5)  throw "too low";
        if(x > 10)   throw "too high";
      }
      catch(err) {
        message.innerHTML = "Input is " + err;
      }
    ```
    
      
    

## Functions

```JavaScript
function getData(param1, param2) {
	// do something
	return something
}
```

Functions can be defined ==inside== other functions:

```JavaScript
const getData = () => {
	const dosomething = () => {}
	dosomething()

	return 'test'
}
```

> [!important] The
> 
> ==nested== function ==cannot== be called from the ==outside== of the enclosing function. We can also `return` a function from a function

  

### ==**Generator function**==

The `**function***` declaration creates a **==[binding](https://developer.mozilla.org/en-US/docs/Glossary/Binding)==** of a new generator function to a given name. A generator function can be exited and later re-entered, with its context (variable [bindings](https://developer.mozilla.org/en-US/docs/Glossary/Binding)) saved across re-entrances.

```JavaScript
function* generator(i) {
  yield i;
  yield i + 10;
}

const gen = generator(10);

console.log(gen.next().value);
// Expected output: 10

console.log(gen.next().value);
// Expected output: 20
```

## Arrow Functions

```JavaScript
let getData = function() {
	//...
}
getData()
```

That's the same thing we do with arrow functions:

```JavaScript
let getData = () => {
	//...
}
getData()
```

If you have one (and just one) parameter, you could omit the parentheses completely:

```JavaScript
const getData = param => console.log(param)
```

Arrow functions allow you to have an ==implicit return==: values are returned ==without== having to use the `return` keyword.

```JavaScript
const getData = () => 'test'
getData() //'test'
```

  

## Objects

```JavaScript
const car = {}
```

You can also use the `new Object` syntax:

```JavaScript
const car = new Object()
```

  

You can also initialize an object using the `new` keyword before a function with a capital letter. This function serves as a constructor for that object.

```JavaScript
function Car(brand, model) {
	this.brand = brand
	this.model = model
}

const myCar = new Car('Ford', 'Fiesta')
myCar.brand //'Ford'
myCar.model //'Fiesta'
```

  

> [!important] Objects are always passed by reference.

```JavaScript
let age = 36
let myAge = age
myAge = 37
age //36
```

but

```JavaScript
const car = {
	color: 'blue'
}
const anotherCar = car
anotherCar.color = 'yellow'
car.color //'yellow'
```

  

### ==Object properties==

```JavaScript
const car = {
	brand: {
		name: 'Ford'
	},
	color: 'blue'
}
```

In this example, you can access the brand name using

```JavaScript
car.brand.name
```

or

```JavaScript
car['brand']['name']
```

  

You can delete a property from this object using

```JavaScript
delete car.brand
```

  

### ==Object methods==

```JavaScript
const car = {
	brand: 'Ford',
	model: 'Fiesta',

	start: function() {
		console.log(`Started
		${this.brand} ${this.model}`)
	}

}

car.start()
```

> [!important] It's important to note this distinction between
> 
> ==regular functions== and ==arrow== ==functions==: we ==don't== have access to `this` if we use an arrow function

  

### ==**JavaScript Object Accessors**==

Provides a **simplier** syntax.

- **Getters**

```JavaScript
// Create an object:
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "en",
  get lang() {
    return this.language;
  }
};

// Display data from the object using a getter:
document.getElementById("demo").innerHTML = person.lang;
```

- **Setters**

```JavaScript
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "",
  set lang(lang) {
    this.language = lang;
  }
};

// Set an object property using a setter:
person.lang = "en";

// Display data from the object:
document.getElementById("demo").innerHTML = person.language;
```

  

### ==Object Constructor==

```JavaScript
function Person(first, last, age, eye) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eye;
}
```

  

### ==Object Prototypes==

The JavaScript `prototype` property allows you to ==add== new ==properties== to object constructors

```JavaScript
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.nationality = "English";
Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};
```

  

### `call()` ==Method==

With `call()`, an object can use a method belonging to ==another object==.

```JavaScript
const person = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
const person1 = {
  firstName:"John",
  lastName: "Doe"
}
const person2 = {
  firstName:"Mary",
  lastName: "Doe"
}

// This will return "John Doe":
person.fullName.call(person1);
```

  

### `apply()` ==Method==

similar to the `call()` method

The Difference Between call() and apply()

- The `call()` method takes arguments ==**separately**==
- The `apply()` method takes arguments as an ==**array**==

```JavaScript
const person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}

const person1 = {
  firstName:"John",
  lastName: "Doe"
}

person.fullName.apply(person1, ["Oslo", "Norway"]);
```

  

### `bind()` ==Method==

With the `bind()` method, an object can **==borrow==** a method from ==another object==

```JavaScript
const person = {
  firstName:"John",
  lastName: "Doe",
  fullName: function () {
    return this.firstName + " " + this.lastName;
  }
}

const member = {
  firstName:"Hege",
  lastName: "Nilsen",
}

let fullName = person.fullName.bind(member);
```

## Classes

```JavaScript
class Person {
	constructor(name) {
		this.name = name
	}

	hello() {
	return 'Hello, I am ' + this.name + '.'
	}
}
```

You can define a method as `static` to allow it to be executed on the class instead:

```JavaScript
class Person {
	static genericHello() {
	return 'Hello'
	}
}

Person.genericHello() //Hello
```

  

## Inheritance

```JavaScript
class Programmer extends Person {
	hello() {
		return super.hello() +
		'. I am also a programmer.'
	}
}

const flavio = new Programmer()
flavio.hello() //Hello, I am a Person. I am also a programmer.
```

## Asynchonous Programming and Callbacks

> [!important] Most of the time, JavaScript code is ran
> 
> ==synchronously==. This means that a line of code is executed, then the next one is executed, and so on
> 
> However there are times when you cannot just wait for a line of code to execute. JavaScript solves this problem using ==**callbacks**==

- One of the simplest examples of how to use callbacks is timers
    
    The `setTimeout()` function accepts 2 arguments: a function, and a number. The number is the milliseconds that must pass before the function is ran.
    
    ```JavaScript
    setTimeout(() => {
    	// runs after 2 seconds
    	console.log('inside the function')
    }, 2000)
    ```
    
      
    
    Take an example:
    
    ```JavaScript
    console.log('before')
    
    setTimeout(() => {
    	// runs after 2 seconds
    	console.log('inside the function')
    }, 2000)
    
    console.log('after')
    ```
    
    This happening in your console:
    
    ```JavaScript
    before
    after
    inside the function
    ```
    
    > [!important] The callback function is executed asynchronously.
    > 
    >   
    > This is a very common pattern when working with the file system, the network, events, or the [[DOM]] in the browser.  
    
      
    
    ### When a function is used as a callback, `**this**` is lost.
    
    ```JavaScript
    const person = {
      firstName:"John",
      lastName: "Doe",
      display: function () {
        let x = document.getElementById("demo");
        x.innerHTML = this.firstName + " " + this.lastName;
      }
    }
    
    setTimeout(person.display, 3000); //undefined
    ```
    
    The `bind()` method solves this problem.
    
    ```JavaScript
    let display = person.display.bind(person);
    setTimeout(display, 3000); //John Doe
    ```
    
      
    
      
    

## Promises

Promises are an alternative way to deal with asynchronous code.

As we saw in the previous chapter, with callbacks we'd be passing a function to another function call, that would be called when the function has finished processing

The main problem with this approach is that if we need to use the result of this function in the rest of our code, all our code must be nested inside the callback, and if we have to do 2-3 callbacks we enter in what is usually defined callback hell with many levels of functions indented into other functions:

```JavaScript
doSomething(result => {
	doSomethingElse(anotherResult => {
		doSomethingElseAgain(yetAnotherResult => {
			console.log(result)
		})
	})
})
```

  

**Promises** are one way to deal with this.

We first call the function, then we have a `then()` method that is called when the function ends. common to detect errors using a `catch()` method

```JavaScript
doSomething()
	.then(result => {
		console.log(result)
	})
	.catch(error => {
		console.log(error)
	})
```

  

Now, to be able to use this syntax, the `doSomething()` function  
implementation must be a little bit special. It must use the Promises API.  

```JavaScript
const doSomething = new Promise(
	(resolve, reject) => {
		//some code
		const success = /* ... */
		if (success) {
			resolve('ok')
		} else {
			reject('this error occurred')
		}
	}
)
```

This function receives 2 parameters. The first is a function we call to resolve the promise, the second a function we call to reject the promise

  

## Async & Await

**Async** functions are a higher level abstraction over promises. An async function `return` a promise

```JavaScript
const getData = () => {
	return new Promise((resolve, reject) => {
		setTimeout(() =>
			resolve('some data'), 2000)
	})
}
```

Any code that want to use this function will use the `async` keyword right  
before the function.  

```JavaScript
const doSomething = async () => {
	const data = await getData()
	console.log(data)
}
```

> [!important] Whenever we use the
> 
> `await` keyword, we must do so inside a function defined as `async`. The `await` keyword mean the code have to wait the function right after finished and then do the next step.

  

Here is a typical example of this:

```JavaScript
const getFirstUserData = async () => {
	// get users list
	const response = await fetch('/users.json')
	// parse JSON
	const users = await response.json()
	// pick first user
	const user = users[0]
	// get user data
	const userResponse = await fetch(`/users/${user.name}`)
	// parse JSON
	const userData = await user.json()

	return userData
}

getFirstUserData()
```

  

## Variables Scope

> [!important] Scope is the set of variables that’s visible to a part of the program.

- A variable defined as `var` inside a function is only visible inside that function.
- A variable defined as `const` or `let` on the other hand is only visible inside the **block** where it is defined.

> [!important] A
> 
> **block** is a set of instructions grouped into a pair of curly braces, like the ones we can find inside an `if` statement or a `for` loop. And a function, too.

  

### Taking an example:

```JavaScript
function getData() {
  if (true) {
    var data = 'some data'
  }
  console.log(data)
	//some data
}
```

### But

```JavaScript
function getData() {
  if (true) {
    let data = 'some data'
  }
  console.log(data)
	//error: ReferenceError: data is not defined.
}
```

  

## JavaScript Modules

> [!important] JavaScript modules allow you to break up your code into separate files.

### **Modules**

```JavaScript
<script type="module">
	import message from "./message.js";
</script>
```

### Export

Modules with ==**functions**== or ==**variables**== can be stored in any external file.

There are two types of exports: 

- **Named Exports**

```JavaScript
export const name = "Jesse";
export const age = 40;

//or
const name = "Jesse";
const age = 40;

export {name, age};
```

- **Default Exports**

```JavaScript
const message = () => {
	const name = "Jesse";
	const age = 40;
	return name + ' is ' + age + 'years old.';
};

export default message;
```

## Import

- Import ==Named exports== 
    
    ```JavaScript
    import { name, age } from "./person.js";
    ```
    
- Import ==Default exports==
    
    ```JavaScript
    import message from "./message.js";
    ```
    

## JavaScript JSON

> [!important] **==JSON==**
> 
> is a format for storing and transporting ==data==.
> 
> **==JSON==** is often used when ==data== is sent from a ==server== to a web page.

### What is JSON?

- **JSON** stands for ==**J**====ava====**S**====cript== ==**O**====bject== ==**N**====otation==
- **JSON** is a lightweight ==data== interchange format
- **JSON** is language independent 
- **JSON** is "self-describing" and easy to understand

```JavaScript
{
	"employees":[
		  {"firstName":"John", "lastName":"Doe"},
		  {"firstName":"Anna", "lastName":"Smith"},
		  {"firstName":"Peter", "lastName":"Jones"}
	]
}
```

## JavaScript Performance

### **Reduce Activity in Loops**

> [!important] Each statement in a loop, including the for statement, is executed for each iteration of the loop.
> 
> Statements or assignments that can be placed outside the loop will make the loop run faster.

Taking an example:

```JavaScript
//Bad:
for (let i = 0; i < arr.length; i++) {}


//Better Code:
let l = arr.length;
for (let i = 0; i < l; i++) {}
```

  

### **Reduce DOM Access**

> [!important] Accessing the
> 
> **HTML DOM** is very slow, compared to other JavaScript statements.

If you expect to access a DOM element several times, access it once, and use it as a local **variable**:

```JavaScript
const obj = document.getElementById("demo");
obj.innerHTML = "Hello";
```

  

### Reduce DOM size

> [!important] Keep the number of elements in the HTML DOM small.
> 
> This will always improve page loading, and speed up rendering (page display), especially on smaller devices.
> 
> Every attempt to search the DOM (like getElementsByTagName) will benefit from a smaller DOM.

### **Avoid Unnecessary Variables**

> [!important] **Don't**
> 
> create new variables if you don't plan to save values.

  

### **Delay JavaScript Loading**

Putting your scripts at the bottom of the page body lets the browser load the page first.

> [!important] An alternative is to use 
> 
> `defer="true"` in the script tag. The defer attribute specifies that the script should be executed after the page has finished parsing, but it only works for external scripts.

## Naming convention

> [!info] GitHub - kettanaito/naming-cheatsheet: Comprehensive language-agnostic guidelines on variables naming. Home of the A/HC/LC pattern.  
> Comprehensive language-agnostic guidelines on variables naming.  
> [https://github.com/kettanaito/naming-cheatsheet?tab=readme-ov-file#naming-convention](https://github.com/kettanaito/naming-cheatsheet?tab=readme-ov-file#naming-convention)  

> [!info] GitHub - TobitSoftware/react-project-guideline: Defines a consistent structure for React projects.  
> Defines a consistent structure for React projects.  
> [https://github.com/TobitSoftware/react-project-guideline#naming-conventions](https://github.com/TobitSoftware/react-project-guideline#naming-conventions)

## Related

- [[ES5 vs ES6]] - ECMAScript version differences
- [[TypeScript]] - Typed superset of JavaScript
- [[NodeJS]] - Server-side JavaScript runtime
- [[React]] - UI library built on JavaScript
- [[DOM]] - Browser document object model