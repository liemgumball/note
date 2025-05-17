## **Function Type Expressions**

The simplest way to describe a function is with a *function type expression*. These types are syntactically similar to arrow functions:

```tsx
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}
 
function printToConsole(s: string) {
  console.log(s);
}
 
greeter(printToConsole);
```

## **Call Signatures**

In JavaScript, functions can have properties in addition to being callable. However, the function type expression syntax doesn’t allow for declaring properties. If we want to describe something callable with properties, we can write a *call signature* in an object type

```tsx
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
 
function myFunc(someArg: number) {
  return someArg > 3;
}
myFunc.description = "default description";
 
doSomething(myFunc);
// default description returned true
```

<aside>
⚠️ Note that the syntax is slightly different compared to a function type expression - use `:` between the parameter list and the return type rather than `=>`.

</aside>

## **Construct Signatures**

JavaScript functions can also be invoked with the `new` operator. TypeScript refers to these as *constructors* because they usually create a new object.

```tsx
type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}
```

## Generic Functions

In **TypeScript**, *generics* are used when we want to describe a correspondence between two values (`input` & `output`). We do this by declaring a *type parameter* in the function signature:

```tsx
function firstElement<Type>(arr: Type[]): Type | undefined {
	return arr[0];
}
```

<aside>
💡 Note that we didn’t have to specify `Type` in this sample. The type was *inferred* - chosen automatically - by TypeScript.

</aside>

We can use multiple type parameters as well.

```tsx
function map<Input, Output>(
	arr: Input[],
	func: (arg: Input) => Output
): Output[] {
  return arr.map(func);
}

// Parameter 'n' is of type 'string'
// 'parsed' is of type 'number[]'
const parsed = map(["1", "2", "3"], (n) => parseInt(n))
```

## Contraints

Sometimes we want to relate two values, but can only operate on a certain subset of values. In this case, we can use a *constraint* to limit the kinds of types that a type parameter can accept.

```tsx
function longest<Type extends { length: number }>(
	a: Type,
	b: Type
) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}
 
// longerArray is of type 'number[]'
const longerArray = longest([1, 2], [1, 2, 3]);
// longerString is of type 'alice' | 'bob'
const longerString = longest("alice", "bob");
// Error! Numbers don't have a 'length' property
const notOK = longest(10, 100);
//Argument of type 'number' is not assignable
// to parameter of type '{ length: number; }'.
```

Because we constrained `Type` to `{ length: number }`, we were allowed to access the `.length` property of the `a` and `b` parameters.

## **Specifying Type Arguments**

**TypeScript** can usually infer the intended type arguments in a generic call, but not always. Normally it would be an error to call this function with mismatched arrays

```tsx
function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
  return arr1.concat(arr2);
}

const arr = combine([1, 2, 3], ["hello"]);
// Type 'string' is not assignable to type 'number'.
```

however, we could manually specify `Type`

```tsx
const arr = combine<string | number>([1, 2, 3], ["hello"]);
```

<aside>
📌 **Rule** When possible, use the type parameter itself rather than constraining it

</aside>

```tsx
//good
function firstElement1<Type>(arr: Type[]) {
  return arr[0];
}

 //bad
function firstElement2<Type extends any[]>(arr: Type) {
  return arr[0];
}
```

---

<aside>
📌

**Rule** Always use as few type parameters as possible

</aside>

Let’s take this example

```tsx
//good
function filter1<Type>(
	arr: Type[],
	func: (arg: Type) => boolean
): Type[] {
  return arr.filter(func);
}
 

//bad
function filter2<Type, Func extends (arg: Type) => boolean>(
  arr: Type[],
  func: Func
): Type[] {
  return arr.filter(func);
}
```

Created a type parameter `<Func>` that *doesn’t relate two values*. That’s always a **red flag** ⛳, because it means callers wanting to specify type arguments have to manually specify an extra type argument for no reason.

## **Optional Parameters**

```tsx
function f(x?: number) {
  // ...
}
f(); //OK
f(10); //OK
```

<aside>
📌 **Rule** When writing a function type for a callback, *never* write an optional parameter unless you intend to *call* the function without passing that argument

</aside>

```tsx
function myForEach(
	arr: any[],
	callback: (arg: any, index?: number) => void
) {
  for (let i = 0; i < arr.length; i++) {
    callback(arr[i], i);
  }
}

//call
myForEach([1, 2, 3], (a, i) => {
  console.log(i.toFixed());
	//'i' is possibly 'undefined'.
});
```

## Function Overloads

In **TypeScript**, we can specify a function that can be called in different ways by writing *overload signatures*

```tsx
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
function makeDate(
	mOrTimestamp: number,
	d?: number,
	y?: number
): Date {
  if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
  } else {
    return new Date(mOrTimestamp);
  }
}
const d1 = makeDate(12345678);
const d2 = makeDate(5, 5, 5);
const d3 = makeDate(1, 3);
// No overload expects 2 arguments,
// but overloads do exist that expect either 1 or 3 arguments.
```

### **Overload Signatures and the Implementation Signature**

<aside>
💡 The signature of the *implementation* is not visible from the outside. When writing an overloaded function, you should always have *two* or more signatures above the implementation of the function.

</aside>

Example 1

```tsx
function fn(x: boolean): void;
// Argument type isn't right
function fn(x: string): void;
// This overload signature is not compatible with
// its implementation signature.

function fn(x: boolean) {}
```

Example 2

```tsx
function fn(x: string): string;
// Return type isn't right
function fn(x: number): boolean;
// This overload signature is not compatible with
// its implementation signature.

function fn(x: string | number) {
  return "oops";
}
```

Good Overloads

```tsx
function len(s: string): number;
function len(arr: any[]): number;
function len(x: any) {
  return x.length;
}
```

<aside>
💡 Always prefer parameters with union types instead of overloads when possible

</aside>

## Declaring `this` in a Function

```tsx
const user = {
  id: 123,
 
  admin: false,
  becomeAdmin: function () {
    this.admin = true;
  },
};
```

TypeScript understands that the function `user.becomeAdmin` has a corresponding `this` which is the outer object `user`

but

there are a lot of cases where you need more control over what object `this` represents.

```tsx
interface User {
  id: number;
  admin: boolean;
}
declare const getDB: () => DB;

interface DB {
  filterUsers(filter: (this: User) => boolean): User[];
}
 
const db = getDB();
const admins = db.filterUsers(function (this: User) {
  return this.admin;
});
```

## **Other Types to Know About**

- `void`
- `object` (not global `Object`)
- `unknow` similar to the `any`
- `never`: represents values which are *never* observed. In a return type, this means that the function throws an exception or terminates execution of the program.
    
    ```tsx
    function fail(msg: string): never {
      throw new Error(msg);
    }
    ```
    
- `Function` (global)

## **Rest Parameters and Arguments**

1. **Rest Parameters**
    
    A rest parameter appears after all other parameters, and uses the `...` syntax
    
    ```tsx
    function multiply(n: number, ...m: number[]) {
      return m.map((x) => n * x);
    }
    
    const a = multiply(10, 1, 2, 3, 4); // [10, 20, 30, 40]
    ```
    
2. **Rest Arguments**
    
    Conversely with **Rest Parameters**, we can *provide* a variable number of arguments from an iterable object (for example, an array) using the spread syntax `...`
    
    ```tsx
    const arr1 = [1, 2, 3];
    const arr2 = [4, 5, 6];
    arr1.push(...arr2);
    ```
    

<aside>
💡 **Note** that in general, TypeScript does not assume that arrays are immutable. This can lead to some surprising behavior

</aside>

```tsx
const args = [8, 5];
const angle = Math.atan2(...args);
// A spread argument must either have a tuple type
// or be passed to a rest parameter.

// OK
const args = [8, 5] as const;
const angle = Math.atan2(...args);
```

## **Parameter Destructuring**

Use *parameter destructuring* to conveniently unpack objects provided as an argument into one or more local variables in the function body

```tsx
function sum({ a, b, c }: { a: number; b: number; c: number }) {
  console.log(a + b + c);
}
```

```tsx
// Same as prior example
type ABC = { a: number; b: number; c: number };
function sum({ a, b, c }: ABC) {
  console.log(a + b + c);
}
```

## **Assignability of Functions**

### Return type `void`

Contextual typing with a return type of `void` does **not** force functions to **not** return something. Another way to say this is a contextual function type with a `void` return type (`type voidFunc = () => void`), when implemented, can return `*any`* other value, but it will be **ignored**.

```tsx
type voidFunc = () => void;
 
const f1: voidFunc = () => {
  return true;
};

f1(); //type 'void'
```

<aside>
⚠️ When a literal function definition has a `void` return type, that function must **not** return anything.

</aside>

```tsx
function f2(): void {
  // @ts-expect-error
  return true;
}
 
const f3 = function (): void {
  // @ts-expect-error
  return true;
};
```