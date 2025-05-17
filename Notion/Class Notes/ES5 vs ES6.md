Created: July 12, 2023 1:51 PM
Class: Agility IO InternShip
Type: Front-end
Materials: https://www.javatpoint.com/es5-vs-es6, https://www.w3schools.com/Js/js_versions.asp
Reviewed: Yes
Edited: May 10, 2025 2:46 PM

# Required
- [JavaScript](JavaScript.md)


# Difference between ES5 and ES6

## ES5

ES5 is the fifth edition of the **ECMAScript. Introduced in 2009**

## ES6

ES6 is the sixth edition of the **ECMAScript. Introduced in 2015**

## Data types

In **ES5** supports primitive data types that are **`string`, `number`, `boolean`, `null`,** and **`undefined`**.

In **ES6**, there are some additions to **JavaScript** data types. It introduced a new primitive data type **`symbol`** for supporting unique values.

## Variables

We could only define the variables by using the **`var`** keyword.

There are two new ways to define variables that are **`let`** and **`const`** uses **block scope**

```jsx
{
  let x = 2;
	const y = 3;
	var z = 4;
}
// x, y can NOT be used here
// z can be used here
```

## Arrow Functions

In **ES5**, both **`function`** and **`return`** keywords are used to define a function.

An **arrow function** is a feature introduced in ES6 by which we don't require the **`function`** keyword

```jsx
// in ES5
function square(num) {
  return num * num;
}
// in ES6
var square = (num) => {
  return num * num;
};
// equivalent way ES6
var square = (num) => num * num;
```

## Spread operator `(…)`

It is introduced in **ES6**, which makes it easy to merge arrays and objects.

```jsx
var target = { name: "xyz", age: 20 };
var source1 = { name: "abc", grade: 12 };
var source2 = { gender: "female" };

//In ES5
updatedTarget = Object.assign(target, source1, source2);
console.log(updatedTarget, target);
//{ name: 'abc', age: 20, grade: 12, gender: 'female' }
//{ name: 'abc', age: 20, grade: 12, gender: 'female' }

// In ES6
updatedTarget = { ...target, ...source1, ...source2 };
console.log(updatedTarget, target);
//{ name: 'abc', age: 20, grade: 12, gender: 'female' }
//{ name: 'xyz', age: 20 }
```

## **Object Destructuring**

Before **ES6**, we had to extract objects manually, which is time-consuming, and it takes more lines of code as well. **ES6** introduced an elegant way of unpacking object properties.

```jsx
var object = { name: "liem", age: 22, grade: 4, gender: "male" };

// ES5
var name = object.name;
var age = object.age;
var grade = object.grade;
var gender = object.gender;

// ES6
var { name, age, grade, gender } = object;
```

## Defining Objects

```jsx
var name = "liem";
var age = 22;
var grade = 4;
var gender = "male";

// ES5
var object1 = { name: name, age: age, grade: grade, gender: gender };
// ES6
var object2 = { name, age, grade, gender };
```

## Module Export

```jsx
var myTestModule = { name: "liem", age: 22, grade: 4, gender: "male" };

// ES5
module.exports = myTestModule;

// ES6
export default myTestModule;

// ES6
export const name = "liem";
export const age = 22;
```

## Module Import

```jsx
//ES5
var myTestModule = require("./myTestModule");

//ES6
import myTestModule from "./myTestModule";

// ES6 import child modules
import { name, age } from "./myTestModule";
```

## String I**nterpolation**

**ES6** introduced a new feature known as **Template Literal ```** that allows us to perform string interpolation more conveniently.

```jsx
var name = "liem";
var age = 22;
var grade = 4;

// ES5
var str = name + " is " + age + " years old and studying in grade " + grade;

// ES6
var str = `${name} is ${age} years old and studying in grade ${grade}`;
```

## **Callbacks and Promises**

Consider a simple example that checks whether the `user` has access or not.

### ES5

```jsx
var access = true;
function callback(message) {
  console.log("Success!" + message);
}

function errorCallback(message) {
  console.log("Failed!" + message);
}

function test(callback, errorCallback) {
  if (access) {
    callback("You do have access");
  } else {
    errorCallback("You don't have access");
  }
}
```

### ES6

```jsx
var access = true;
function test1() {
  return new Promise((resolve, reject) => {
    if (access) {
      resolve("You do have access");
    } else {
      reject("You don't have access");
    }
  });
}

test1()
  .then((message) => console.log("Success!" + message))
  .catch((message) => console.log("Failed!" + message));
```