---
Created: 2024-07-27T22:02
Class: mgm
Type: Front-end
Reviewed: false
Edited: 2024-12-03T11:29
---
# Generics

> [!important] **Generics**
> 
> allows for improved reusability by parameterizing a type with another one.

## Generics versus `any`

```TypeScript
const a: Array<string> = new Array("abc", "def");
const s: string = a[0]; // No cast required
console.log(s.substr(0,1)); // Access to string members
```

```TypeScript
const a2: Array<any> = new Array("abc", "def");
const s2 = a2[0]; // No cast required
console.log(s2.substringg(0, 1)); // TypeScript does not safe guard
```

## Default for the Generic Type

```TypeScript
interface MyGenericWithDefault<T = string> {
    myTypeWhichIsStringIfNotSpecified: T;
}

const myGeneric1: MyGenericWithDefault<number> = { myTypeWhichIsStringIfNotSpecified: 1 };
const myGeneric2: MyGenericWithDefault = { myTypeWhichIsStringIfNotSpecified: "string" };
const myGeneric3: MyGenericWithDefault<string> = { myTypeWhichIsStringIfNotSpecified: "string" };
```

## Generic Functions

Making **Generic function** a way of saying “_this function works with any kind of array_” and while maintaining type safety at the same time.

```TypeScript
function map<TElement, TResult>(
  items: TElement[],
  mappingFunction: (item: TElement) => TResult
): TResult[] {
  /* ... */
}
```

## Generic Interfaces

```TypeScript
interface Form<T> {
  values: T;
}
 
interface Contact {
  name: string;
  email: string;
}
 
const contactForm: Form<Contact> = {
  values: {
    name: "Bob",
    email: "bob@someemail.com"
  }
}
```

We are going to expand the `Form` interface to include a property for the form’s ==validation errors==.

```TypeScript
interface Form<T> {
  errors: {
    [P in keyof T]?: string;
  };
  values: T;
}
```

This is an advanced type that we haven’t covered so far. So, let’s break this down:

- The type is in curly brackets, so we are constructing an object type.
- `[P in keyof T]` will put all the keys in the type `T` into a string literal union. This will be `"name" | "email"` for `contactForm`.
- `[P in keyof T]` "computes" the property name of the object being constructed. So, for `contactForm`, the properties in the object are `name` and `email`.
- The `?` after the property name means the properties are optional.
- The type for the properties is `string`.
- So, for `contactForm`, the type for the errors is `{name?: string; email?: string}`.

  

1. Add an empty `errors` object to our `contactForm` object.

```TypeScript
const contactForm: Form<Contact> = {
 errors: {},
 values: { ... }
};
```

1. Add an `error` for the email contact

```TypeScript
const contactForm: Form<Contact> = {
 errors: {
   email: "This must be a valid email address"
 },
 values: { ... }
};
```

## Case Studies

### **Dependency Inversion Principle**

**OOP** interfaces are often used to fulfill the **Dependency Inversion Principle** from [SOLID](https://deviq.com/solid/) design principles.

```TypeScript
interface LogginService {
	log(message: string): void;
}

class ServerLoggingService implements LoggingService {
	log(message: string): void {
		// send logs to server
	}
```

### Generic OOP interfaces

An interface can specify a list of methods that must be provided by the implementation. A ==**generic interface**== is very similar with the exception that some of the methods can be generic.

```TypeScript
interface Observer<T> {
	closed?: boolean;
	next: (value: T) => void;
	error: (err: any) => void;
	complete: () => void;
}
```

```TypeScript
interface ReadonlyArray<T> {
    // Skipped most of the methods for brevity.
    slice(start?: number, end?: number): T[];
    map<U>(callbackfn: (value: T, index: number, array: readonly T[]) => U, thisArg?: any): U[];
    reduce<U>(callbackfn: (previousValue: U, currentValue: T, currentIndex: number, array: readonly T[]) => U, initialValue: U): U;
    readonly [n: number]: T;
}
```

## Generic and Classes

```TypeScript
// Three classes that inherit a common one
interface Greeter {
    greeting: string;
}
class Human implements Greeter { // Implement the common interface
    public greeting: string = "Hello";
}
class Lion implements Greeter {// Implement the common interface
    public greeting: string = "Grrrrrr";
}
class Tulip { // Does not implement the common interface
    public greeting: string = "...";
}
 
// Not limited to Human! Now any type that inherits Greeter
class LivingSpecies {
    public species: Greeter;
 
    constructor(species: Greeter) {
        this.species = species;
    }
    public sayHello(): void {
        console.log(this.species.greeting);
    }
}
const species1 = new LivingSpecies(new Human());
species1.sayHello();
const species2 = new LivingSpecies(new Lion());
species2.sayHello();
const species3 = new LivingSpecies(new Tulip());
species3.sayHello();
```

## Using some standard generic types

1. `Array<ItemType>`
2. `Promise<ReturnType>`

### Type Argument Propagation

```TypeScript
interface Person {
	id: string;
	name: string;
	birthYear: number;
}

function getIds<T extends Record<'id', string>>(elements: T[]) {
	return elements.map(ele => ele.id);
}
```

This example code is quite verbose. But we can make it more concise by taking advantage of a functional programming technique call `**pointfree style**`.

```TypeScript
import * as R from 'ramda';

const getIds = R.map(R.prop('id'));
```

`map` is partially applied with a mapper function, `prop` which extracts the `id` property from and object.

> [!important] This is where 
> 
> _==propagated generic type arguments==_ come in.

## Generic Comparison

### Generic and `typeof`

> [!important] The generic code does not allow the use of
> 
> `typeof` on `T` , `new T` , or `instanceof T`

### The Generic solution

To compare 2 generics, we need to keep in mind that the types are removed when TypeScript is transpiled to JavaScript. Thus, we need to create a custom generic array with a unique identifier for comparison.

```TypeScript
class IdentificatedGeneric<S> extends Array<S> {
    public id: string; // Enhancement of Array class
    public constructor(id: string) {
        super();
        this.id = id;
    }
}

function concatenate<S, T1 extends IdentificatedGeneric<S>>(list1: T1, list2: T1): T1 {
    if (list1.id === list2.id) { // Comparison to ensure from the same id, possible because both extends IdentificatedGeneric
        const oneList = [...list1, ...list2] as T1;
        return oneList;
    }
    throw Error("Must be the same id");
}
 
const l1 = new IdentificatedGeneric<string>("l1");
const l2 = new IdentificatedGeneric<string>("l2");
const l3 = new IdentificatedGeneric<number>("l1");
const l4 = new IdentificatedGeneric<string>("l1");
 
l1.push("1", "2");
l2.push("100", "200");
l3.push(5, 6);
l4.push("500", "600");
 
// const c1 = concatenate(l1, l2); // Error 1
// console.log(c1);
// const c2 = concatenate(l1, l3); // Error 2
// console.log(c2);
const c3 = concatenate(l1, l4);
console.log(c3);
```

### Generic with Construction Function

```TypeScript
interface IMyInterfaceWithConstructor<T> {
    new(param: string): T; // Force to have a constructor with the signature of 1 parameter that is a string
}
 
function createInstance<T>(ctor: IMyInterfaceWithConstructor<T>, param1: string): T { // Create a new type T
    return new ctor(param1);
}
 
class C1 {
    constructor(name: string) { // We can create from createInstance function because 1 parameter and string
        console.log("Initializing class C1 with string: " + name);
    }
}
 
class C2 {
    constructor(name: string) { // We can create from createInstance function because 1 parameter and string
        console.log("Initializing class C2 with string: " + name);
    }
}
 
const inst1 = createInstance(C1, "Instance 1");
const inst2 = createInstance(C2, "Instance 2");
```

---

# Narrowing

## Type Narrowing with `in`

> [!important] **The**
> 
> `**in**` **operator explained**  
> The   
> `in` operator can narrow a type from a union. The left part of the operand is a string or a string literal. The right part is a union type. The result is a `Boolean`that returns `true` if the union contains the string and `false` if it doesn’t.

```TypeScript
interface IN_A {
    m1: number;
    m2: boolean;
}
interface IN_B {
    m3: string;
}
 
function foo(x: IN_A | IN_B) {
    if ("m1" in x) { // m1 is only in IN_A
        console.log("Type narrowed to IN_A", x.m1, x.m2);
    } else { // IN_B
        console.log("Type narrowed to IN_B", x.m3);
    }
    console.log("A is still IN_A or IN_B");
}
 
foo({ m1: 1, m2: true }); // Implicit IN_A
foo({ m3: "" }); // Implicit IN_B
```

## **Custom Type Guards**

```TypeScript
interface Article {
  title: string;
  content: string;
}
 
function isArticle(object: any): object is Article {
  return "title" in object && "content" in object;
}
 
fetch("http://example.com")
  .then(response => response.json())
  .then(body => {
    if (isArticle(body)) {
      return body.title;
    } else {
      throw new Error("This is not an article");
    }
  });
```

---

# Conditional and Mapped Types

## Conditional Types

```TypeScript
type IsString<T> = T extends string ? true : false;
 
type A = IsString<string>; // A === true
type B = IsString<"abc">; // B === true
type C = IsString<123>; // C === false
```

### Conditional Type are Distributive

```TypeScript
type NonNullable<T> = T extends null | undefined ? never : T;

type Foo = NonNullable<string | undefined>; // Foo is string
```

![[Screenshot_2024-07-29_at_15.56.20.png]]

### Nested Type Condition

```TypeScript
type RemoveBoolean<T> = {
  [Key in keyof T]: boolean extends T[Key] ? never : Key // nested condition
}[keyof T];
 
interface Inf1 {
  m1: string;
  m2: boolean;
  m3: number;
}
 
type NoBoolean1 = RemoveBoolean<Inf1>; // "m1" | "m3"
```

### Inferring Conditional Types with `infer`

==**TypeScript 2.8**== brings a new keyword, `infer`. The new addition returns a type from a generic. The role of inferring is to tell **TypeScript** to figure out the type instead of defining the type at the class or function level. Normally, generic requires you to declare the generic type from the start. However, in some situations, the type may not be known.

```TypeScript
type GetReturnedType<T> = T extends (...agrs: any[]) => infer R ? R : T;
 
function whatIsMyReturnType(): number {
    return 1;
}
// number from 'R'
type TypeFromReturn = GetReturnedType<typeof whatIsMyReturnType>;
const dynamicallyTyped: TypeFromReturn = 1;
// number from 'T'
type TypeFromReturn2 = GetReturnedType<number>;
```