Created: August 2, 2023 11:13 AM
Class: Agility IO InternShip
Type: Front-end
Materials: https://www.typescriptlang.org/docs/handbook/
Reviewed: Yes
Edited: May 10, 2025 2:46 PM

# **TypeScript**

<aside>
💡 The most common kinds of errors in **JavaScript** that programmers write can be described as type errors: a certain kind of value was used where a different kind of value was expected.

</aside>

```bash
npm install -g ts-node
```

The goal of **TypeScript** is to be a **static typechecker for JavaScript** programs - in other words, a tool that runs before your code runs (static) and ensures that the types of the program are correct.

[Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

## TypeScript for JavaScript Programmer

TypeScript offers all of JavaScript’s features, and an additional layer on top of these: TypeScript’s type system.

For example, JavaScript provides language primitives like `string` and `number`, but it doesn’t check that you’ve consistently assigned these. TypeScript does.

- Defining Type
- Composing Type

---

# The Basic

<aside>
💡 Each and every value in **JavaScript** has a set of behaviors you can observe from running different operations.

</aside>

For some values, such as the primitives `string` and `number`, we can identify their type at runtime using the `typeof` operator. But for other things like functions, there’s no corresponding runtime mechanism to identify their types.

```jsx
function fn(x) {
  return x.flip();
}
```

We can *observe* by reading the code that this function will only work if given an object with a callable `flip` property, but JavaScript doesn’t surface this information in a way that we can check while the code is running. The only way in pure JavaScript to tell what `fn` does with a particular value is to call it and see what happens

<aside>
⚠️ **This kind of behavior makes it hard to predict what the code will do before it runs!**

</aside>

## Static type-checking

*Static types systems* describe the shapes and behaviors of what our values will be when we run our programs. A **type-checker** like TypeScript uses that information and tells us when things might be going off the rails.

```tsx
const message = "hello!";
 
message();
// This expression is not callable.
// Type 'String' has no call signatures.
```

## **Non-exception Failures**

```jsx
const user = {
  name: "Daniel",
  age: 26,
};

user.location; 

// returns undefined
```

```tsx
const user = {
  name: "Daniel",
  age: 26,
};
 
user.location;
// Property 'location' does not exist on
// type '{ name: string; age: number; }'.
```

Ultimately, a static type system has to make the call over what code should be flagged as an error in its system, even if it’s “**valid**” **JavaScript** that won’t immediately throw an error. In **TypeScript**, the following code produces an error about `location` not being defined

## **Types for Tooling**

TypeScript can catch bugs when we make mistakes in our code. That’s great, but TypeScript can *also* prevent us from making those mistakes in the **first** place.

![Untitled](Notion/Class%20Notes/TypeScript/Untitled.png)

## `tsc`, the TypeScript compiler

```bash
npm install -g typescript
```

## Explicit Types

```bash
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
 
greet("Maddison", new Date());
```

<aside>
💡 We don’t always have to write explicit type annotations. In many cases, **TypeScript** can even just *infer* (or “figure out”) the types for us even if we omit them.

</aside>

![Untitled](Notion/Class%20Notes/TypeScript/Untitled%201.png)

# Everyday Types

### **The primitives**

- `string`
- `number`
- `boolean`

### Array

To specify the type of an array like `[1, 2, 3]`, we can use the syntax `number[]`; this syntax works for any type (e.g. `string[]` is an array of strings, and so on). We may also see this written as `Array<number>`, which means the same thing.

### `any`

TypeScript also has a special type, `any`, that we can use whenever you **don’t** want a particular value to cause typechecking errors.

## **Type Annotations on Variables**

When declaring a variable using `const`, `var`, or `let`, we can optionally add a type annotation to explicitly specify the type of the variable

<aside>
💡 In most cases, though, this isn’t needed. Wherever possible, TypeScript tries to automatically *infer* the types in your code.

</aside>

## **Functions**

TypeScript allows to specify the types of both the input and output values of functions

```tsx
function greet(name: string): number {
  console.log("Hello, " + name.toUpperCase() + "!!");
	return Number(name.lenght)
}
```

### **Anonymous Functions**

It’s a little bit different from function declarations. When a function appears in a place where TypeScript can determine how it’s going to be called, the parameters of that function are automatically given types.

```tsx
const names = ["Alice", "Bob", "Eve"];
 
// Contextual typing for function - parameter s inferred to have type string
names.forEach(function (s) {
  console.log(s.toUpperCase());
});
 
// Contextual typing also applies to arrow functions
names.forEach((s) => {
  console.log(s.toUpperCase());
});
```

Even though the parameter `s` didn’t have a type annotation, TypeScript used the types of the `forEach` function, along with the inferred type of the array, to determine the type `s` will have.

<aside>
📌 This process is called *contextual typing* because the *context* that the function occurred within informs what type it should have.

</aside>

## Object Types

To define an object type, we simply list its properties and their types.

```tsx
function printName(obj: { first: string; last?: string }) {
  // Error - might crash if 'obj.last' wasn't provided!
  console.log(obj.last.toUpperCase()); //'obj.last' is possibly 'undefined'
  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }
 
  // A safe alternative using modern JavaScript syntax:
  console.log(obj.last?.toUpperCase());
}
```

Object types can also specify that some or all of their properties are *optional*. To do this, add a `?` after the property name. And we’ll have to check for `undefined` before using it.

## **Union Types**

TypeScript’s type system allows you to build **new types** out of existing ones using a large variety of operators.

A *union type* is a type formed from two or more other types, representing values that may be *any one* of those types.

```tsx
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
// OK
printId(101);
// OK
printId("202");

// Error
printId({ myID: 22342 });
// Argument of type '{ myID: number; }' is not assignable
// to parameter of type 'string | number'.
```

<aside>
⚠️ TypeScript will only allow an operation if it is valid for *every* member of the union. For example, if you have the union `string | number`, you can’t use methods that are only available on `string`

</aside>

The solution is to *narrow* the union with code, the same as you would in JavaScript without type annotations. *Narrowing* occurs when TypeScript can deduce a more specific type for a value based on the structure of the code.

```tsx
function printId(id: number | string | string[]) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else if(Array.isArray()) {
				console.log("Hello, " + id.join(" and "));
			} else {
		    // Here, id is of type 'number'
		    console.log(id);
		  }
	}
```

## **Type Aliases**

Refer **Object Types** and **Union Types** to it by a single name.

```tsx
type Point = {
  x: number;
  y: number;
};
 
// Exactly the same as the earlier example
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

<aside>
💡 Note that aliases are *only* aliases - you cannot use type aliases to create different/distinct “versions” of the same type.

</aside>

In other words, this code might *look* illegal, but is OK according to TypeScript because both types are aliases for the same type

```tsx
type textInput = string;

function printText(str: string) : textInput {
	console.log(typeof(str)) //string
}

console.log(printText("text")) //string
```

## Interface

An *interface declaration* is another way to name an object type

```tsx
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

### **Differences Between Type Aliases and Interfaces**

Almost all features of an `interface` are available in `type`, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

Extending an interface

```tsx
interface Animal {
  name: string;
}

interface Bear extends Animal {
  honey: boolean;
}

const bear = getBear();
bear.name;
bear.honey;
```

Extending a type via intersections

```tsx
type Animal = {
  name: string;
}

type Bear = Animal & {
  honey: boolean;
}

const bear = getBear();
bear.name;
bear.honey;
```

Adding new fields to an existing interface

```tsx
interface Window {
  title: string;
}

interface Window {
  ts: TypeScriptAPI;
}

const src =
 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```

A type cannot be changed after being created

```tsx
type Window = {
  title: string;
}

type Window = {
  ts: TypeScriptAPI;
}

// Error: Duplicate identifier 
'Window'.
```

## **Type Assertions**

Sometimes you will have information about the type of a value that **TypeScript** can’t know about.

**For example:** if we’re using `document.getElementById`, TypeScript only knows that this will return *some* kind of `HTMLElement`, but we might know that your page will always have an `HTMLCanvasElement` with a given ID.

```tsx
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```

We can also use the angle-bracket syntax (except if the code is in a `.tsx` file)

```tsx
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```

<aside>
🚫 **TypeScript** only allows type assertions which convert to a *more specific* or *less specific* version of a type. This rule prevents “**impossible**” coercions

</aside>

```tsx
const x = "hello" as number;
// Conversion of type 'string' to type 'number' may
// be a mistake because neither type sufficiently overlaps with the other.
// If this was intentional, convert the expression to 'unknown' first.
```

Sometimes this rule can be too conservative and will disallow more complex coercions that might be valid. If this happens, we can use two assertions, first to `any` (or `unknown`, which we’ll introduce later), then to the desired type

```tsx
const a = (expr as any) as T;
```

## **Literal Types**

[Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)

```tsx
let changingString = "Hello World";
changingString = "Olá Mundo";
// Because `changingString` can represent any possible string, that
// is how TypeScript describes it in the type system

const constantString = "Hello World";
// Because `constantString` can only represent 1 possible string, it
// has a literal type representation
```

<aside>
💡 It’s not much use to have a variable that can only have one value!

But by *combining* literals into unions, you can express a much more useful concept

</aside>

```tsx
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "outside");
// Argument of type '"outside"' is not assignable to parameter
// of type '"left" | "right" | "center"'.
```

Of course, we can combine these with non-literal types:

```tsx
interface Options {
  width: number;
}
function configure(x: Options | "auto") {
  // ...
}
configure({ width: 100 });
configure("auto");
configure("automatic");
// Argument of type '"automatic"' is not assignable to parameter
// of type 'Options | "auto"'.
```

### **Literal Inference**

[Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-inference)

When you initialize a variable with an object, TypeScript assumes that the properties of that object might change values later.

```tsx
const obj = { counter: 0 };
if (someCondition) {
  obj.counter = 1;
}
```

`obj.counter` have the type `number`, not `0`, because types are used to determine both *reading* and *writing* behavior.

Same to `string`

```tsx
declare function handleRequest(url: string, method: "GET" | "POST"): void;
 
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method);
// Argument of type 'string' is not assignable
// to parameter of type '"GET" | "POST"'.
```

In the above example `req.method` is inferred to be `string`, not `"GET"`

Because code can be evaluated between the creation of `req` and the call of `handleRequest` which could assign a new string like `"GUESS"` to `req.method`, TypeScript considers this code to have an **error**.

There are two ways to work around this:

- Change the inference by adding a type assertion

```tsx
// Change 1: intend for req.method to always have the literal type "GET"
const req = { url: "https://example.com", method: "GET" as "GET" };

// Change 2: for other reasons that req.method has the value "GET"
handleRequest(req.url, req.method as "GET");
```

- Use `as const` to convert the entire object to be type literals

```tsx
// acts like const
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);
```

<aside>
💡 For the type system, ensuring that all properties are assigned the ***literal type*** instead of a more general version like `string` or `number`.

</aside>

## `null` and `undefined`

JavaScript has primitive values used to signal absent or uninitialized value: `null` & `undefined`

TypeScript has two corresponding *types* by the same names. How these types behave depends on whether you have the [**`strictNullChecks`**](https://www.typescriptlang.org/tsconfig#strictNullChecks) option on or off.

- `strictNullChecks`off
    
    The values that might be `null` or `undefined` can still be accessed normally, and the values `null` and `undefined` can be assigned to a property of any type. This is similar to how languages without null checks (e.g. C#, Java) behave
    
- `strictNullChecks`on
    
    When a value is `null` or `undefined`, you will need to test for those values before using methods or properties on that value. Just like checking for `undefined` before using an optional property, we can use *narrowing* to check for values that might be `null`
    
    ```tsx
    function doSomething(x: string | null) {
      if (x === null) {
        // do nothing
      } else {
        console.log("Hello, " + x.toUpperCase());
      }
    }
    ```
    

<aside>
💡 The lack of checking for these values tends to be a major source of bugs; we always recommend people turn **`strictNullChecks`** on if it’s practical to do so in their codebase.

</aside>

### Non-null Assertion Operator (Postfix `!`)

TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`

```tsx
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

Just like other type assertions, this doesn’t change the runtime behavior of your code, so it’s important to only use `!` when you know that the value *can’t* be `null` or `undefined`.

```tsx
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}

liveDangerously()
// [ERR]: "Executed JavaScript Failed:"
// [ERR]: Cannot read properties of undefined (reading 'toFixed')
```

## `never` and [The `never` type](Narrowing.md)

## `unknow` = a better `any`

The `unknown` type is half a specific explicit type and half the type `any` which allows everything. Declaring a variable as `unknown` allows us to set a wide variety of types without allowing unwanted access to properties or the value of a type.

```tsx
let variable1: any;
variable1 = "It is a string";
console.log(variable1.substr(0,2)) // Output "it"
variable1 = 1;
console.log(variable1.substr(0,2)) // Crash
```

<aside>
📌 Changing the type from `any` to `unknown` indicates to **TypeScript** that the type can receive any value but should be used cautiously. It does not allow the function to be invoked.

</aside>

```tsx
let variable2: unknown;
variable2 = "It is a string";
console.log(variable2.substr(0,2)) // Does not compile here
variable2 = 1;
console.log(variable2.substr(0,2)) // Does not compile here
```

## **Enums**

A feature added to JavaScript by TypeScript which allows for describing a value which could be one of a set of possible named constants. Unlike most TypeScript features, this is *not* a type-level addition to JavaScript but something added to the language and runtime. Because of this, it’s a feature which we should know exists, but maybe hold off on using unless we are sure

[Enums](TypeScript.md) 

# Narrowing

[Narrowing](Narrowing.md)

# More on function

[More on function](More%20on%20function.md)

# Object Type

[Object type](Object%20type.md)

# Type manipulation

[Documentation - Creating Types from Types](https://www.typescriptlang.org/docs/handbook/2/types-from-types.html)

1. Generic
2. `keyof` Type Operator
3. `typeof` Type Operator
4. Indexed access Types
5. Conditional Types
6. Mapped Types
7. Template Literal

# Classes

[Classes](Classes.md)

# Utility Types

[Utility Types](Utility%20Types.md)

# Enums

[Enums](Enums.md)

# Module

**Modules in TypeScript**

```tsx
// @filename: hello.ts
export default function helloWorld() {
  console.log("Hello, world!");
}
```

This is then imported via

```tsx
import helloWorld from "./hello.js";
helloWorld();
```

## **TypeScript Specific ES Module Syntax**

Types can be exported and imported using the same syntax as JavaScript values

```tsx
// @filename: animal.ts
export type Cat = { breed: string; yearOfBirth: number };
 
export interface Dog {
  breeds: string[];
  yearOfBirth: number;
}
 
// @filename: app.ts
import { Cat, Dog } from "./animal.js";
type Animals = Cat | Dog;
```

## **CommonJS Syntax**

### Exporting

Identifiers are exported via setting the `exports` property on a global called `module`

```tsx
// @filename: maths.ts
function absolute(num: number) {
  if (num < 0) return num * -1;
  return num;
}
 
module.exports = {
  pi: 3.14,
  squareTwo: 1.41,
  phi: 1.61,
  absolute,
};
```

### Importing

Then these files can be imported via a `require` statement

```tsx
const maths = require("./maths");
maths.pi;
		// any
```

or

```tsx
const { squareTwo } = require("./maths");
squareTwo;
	// const squareTwo: any
```

# Mixins

[Mixins](Mixins.md)

# Open questions

1. Relationship between Javascript and TypeScript?
    
    **TypeScript** is a language built on top of **JavaScript**, adding *static typing* and *other features* to improve developer *productivity* and *code quality*. It provides a smoother and more organized development experience, especially for larger and more complex projects, while maintaining compatibility with the existing **JavaScript** ecosystem.
    
    - **Syntax Compatibility**
    - **Type Annotations**
    - **Compilation**
    
2. What are TypeScript pros and cons?
    
    **Pros:**
    
    - Static typing catches errors early and improves code quality.
    - Enhanced tooling and IDE support boost developer productivity.
    - Type annotations provide clear documentation and readability.
    - Gradual adoption for existing JavaScript projects.
    - Leverages JavaScript ecosystem and supports modern features.
    
    **Cons:**
    
    - Learning curve for JavaScript developers.
    - Extra compilation step can slow down development.
    - More verbose code due to type annotations.
    - Compatibility issues with some third-party libraries.
    - Potential limitations on dynamic programming patterns.
    
3. What is the difference between types `any` and `Object`?
    - **`any` Type:** It means "anything goes." No type checking is enforced, offering flexibility but sacrificing type safety.
    - **`Object` Type:** Represents all non-primitive types. It allows assignment of various values, but restricts access to specific properties and methods unless type is narrowed down.
    
4. What is Enum type? Which cases will we use Enum?
    
    An **Enum** in **TypeScript** is a data type that lets you define a set of named constants
    
    - **Replacing Magic Numbers**
    - Represent a limited set of valid ***Options* or *Choices***
    - Model different ***States* or *Statuses*:** improving code expressiveness.
    - **Enhancing Readability**
    - **Avoiding Errors**
    
5. What is an Interface in TypeScript?
    
    In **TypeScript**, an interface is a way to define a *contract* or a *structure* that a class or an object must adhere to.
    
    Interfaces play a crucial role in ensuring type *safety*, *providing* a blueprint for how objects should be structured.
    
6. What is the difference between type and interface?
    
    **Interface:**
    
    - Mainly for defining object shapes.
    - Used when classes need to adhere to a specific structure.
    - Can define function and index signatures.
    
    **Type:**
    
    - More flexible, used for complex types, unions, intersections, and aliases.
    - Can define callable signatures.
    - Cannot be extended, but can create aliases for various types.
    
7. What are optional properties in TypeScript?
    
    Optional properties in **TypeScript** are properties within an object type that **may or may not** be present. They're marked with a **`?`** in the type definition.
    
8. What is the default parameters function? What are rest parameters Functions?
    - **Default Parameters Function:**
    Function with predefined default values for its parameters, used when no value is provided during the function call.
    - **Rest Parameters Function:**
    Function that accepts an arbitrary number of arguments as an array, specified using the spread operator **`...`**
        
        Enabling flexibility in handling varying inputs.
        
    
9. What is Named Function?
    
    A named function is a function in programming with a specific name, allowing you to call and reuse it.
    
10. List the cases we should extend the class.
    - Inheritance
    - Specialization
    - Modularity
    - Overriding
    - Polymorphism
    - Interfaces Implementation
    
11. What is the difference between class, interface and abstract class?
    - **Class:** A class is a blueprint for creating objects with properties and methods.
    - **Interface:** An interface defines a contract specifying the structure a class must adhere to.
    - **Abstract Class:** An abstract class is a mix between a class and an interface. It can include method declarations like an interface, but it can also provide default implementations like a class. It cannot be instantiated directly
    
12. List the cases we'll use Decorators, Mixins
    
    **Decorators:**
    
    - **Logging/Debugging**
    - **Validation**
    - **Authorization**
    - **Memoization:** Cache results of expensive function calls to improve performance.
    - **Dependency Injection:** Inject dependencies into classes or functions.
    
    **Mixins:**
    
    - **Code Reuse:** Combine multiple classes' behaviors into a single class without deep inheritance.
    - **Modularity**
    - **Extending Functionality:** Enhance existing classes with additional features.
    - **Avoiding Deep Inheritance**
    
13. List some cases we should use Generic
    - **Reusable Functions/Classes**
    - **Custom Data Structures:** Implement generic data structures like linked lists, trees, or stacks that work with different data types.
    - Design functions that can work with different types of **promises** or **async** operations.
    - Handle varying structures of **API responses** while ensuring type correctness.