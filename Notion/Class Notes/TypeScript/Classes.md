TypeScript offers full support for the `class` keyword introduced in ES2015.

As with other JavaScript language features, TypeScript adds type annotations and other syntax to allow you to express relationships between classes and other types.

```tsx
class Point {
  x: number;
  y: number;
}
 
const pt = new Point();
pt.x = 0;
pt.y = 0;
```

## **`--strictPropertyInitialization`**

The `strictPropertyInitialization` setting controls whether class fields need to be initialized in the constructor.

[TSConfig Reference - Docs on every TSConfig option](https://www.typescriptlang.org/tsconfig#strictPropertyInitialization)

```tsx
class BadGreeter {
  name: string;
//Property 'name' has no initializer and is not definitely assigned in the constructor.
}
```

## `readonly`

Fields may be prefixed with the `readonly` modifier. This prevents assignments to the field outside of the constructor.

```tsx
class Greeter {
  readonly name: string = "world";
 
  constructor(otherName?: string) {
    if (otherName !== undefined) {
      this.name = otherName;
    }
  }
 
  err() {
    this.name = "not ok";
//Cannot assign to 'name' because it is a read-only property.
  }
}
```

## Constructors

> Background Reading:
> 
> 
> [Constructor (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)
> 

Class constructors are very similar to functions. You can add parameters with type annotations, default values, and overloads

There are just a few differences between class constructor signatures and function signatures:

- Constructors can’t have type parameters - these belong on the outer class declaration, which we’ll learn about later
- Constructors can’t have return type annotations - the class instance type is always what’s returned

### Just as in JavaScript, if you have a base class, you’ll need to call `super();` in your constructor body before using any `this.` members

```tsx
class Base {
  k = 4;
}
 
class Derived extends Base {
  constructor() {
    // Prints a wrong value in ES5; throws exception in ES6
    console.log(this.k);
//'super' must be called before accessing 'this' in the constructor of a derived class.
    super();
  }
}
```

## Methods

A function property on a class is called a *method*.

```tsx
let x: number = 0;
 
class C {
  x: string = "hello";
 
  m() {
    // This is trying to modify 'x' from line 1, not the class property
    x = "world";
//Type 'string' is not assignable to type 'number'.
  }
}
```

## **Getters / Setters**

Classes can also have *accessors*

```tsx
class C {
  _length = 0;
  get length() {
    return this._length;
  }
  set length(value) {
    this._length = value;
  }
}
```

TypeScript has some special inference rules for accessors:

- If `get` exists but no `set`, the property is automatically `readonly`
- If the type of the setter parameter is not specified, it is inferred from the return type of the getter
- Getters and setters must have the same [Member Visibility](https://www.typescriptlang.org/docs/handbook/2/classes.html#member-visibility)

## Index Signature

Classes can declare index signatures; these work the same as [Index Signatures for other object types](Object%20type.md)

```tsx
class MyClass {
  [s: string]: boolean | ((s: string) => boolean);
 
  check(s: string) {
    return this[s] as boolean;
  }
}
```

## **Class Heritage**

Like other languages with object-oriented features, classes in JavaScript can inherit from base classes.

### `implements` Clauses

We can use an `implements` clause to check that a class satisfies a particular `interface`. An error will be issued if a class fails to correctly implement it

```tsx
interface Pingable {
  ping(): void;
}
 
class Sonar implements Pingable {
  ping() {
    console.log("ping!");
  }
}
 
class Ball implements Pingable {
// Class 'Ball' incorrectly implements interface 'Pingable'.
// Property 'ping' is missing in type 'Ball' but required in type 'Pingable'.
  pong() {
    console.log("pong!");
  }
}
```

Classes may also implement multiple interfaces

<aside>
📌 **Cautions** It’s important to understand that an `implements` clause is only a check that the class can be treated as the interface type. It doesn’t change the type of the class or its methods *at all*.

</aside>

```tsx
interface Checkable {
  check(name: string): boolean;
}
 
class NameChecker implements Checkable {
  check(s) {
// Parameter 's' implicitly has an 'any' type.
    // Notice no error here
    return s.toLowerCase() === "ok";
  }
}
```

Similarly, implementing an interface with an optional property doesn’t create that property

```tsx
interface A {
  x: number;
  y?: number;
}
class C implements A {
  x = 0;
}
const c = new C();
c.y = 10;
// Property 'y' does not exist on type 'C'.
```

## `extends` Clauses

```tsx
class Animal {
  move() {
    console.log("Moving along!");
  }
}
 
class Dog extends Animal {
  woof(times: number) {
    for (let i = 0; i < times; i++) {
      console.log("woof!");
    }
  }
}

const d = new Dog();
// Base class method
d.move();
// Derived class method
d.woof(3);
```

### **Overriding Methods**

Use the `super.` syntax to access base class methods. Note that because JavaScript classes are a simple lookup object, there is no notion of a “super field”.

```tsx
class Base {
  greet() {
    console.log("Hello, world!");
  }
}
 
class Derived extends Base {
  greet(name?: string) {
    if (name === undefined) {
      super.greet();
    } else {
      console.log(`Hello, ${name.toUpperCase()}`);
    }
  }
}
 
const d = new Derived();
d.greet();
d.greet("reader");
```

### Initialization Order

The order that JavaScript classes initialize can be surprising in some cases. Let’s consider this code:

```tsx
class Base {
  name = "base";
  constructor() {
    console.log("My name is " + this.name);
  }
}
 
class Derived extends Base {
  name = "derived";
}
 
// Prints "base", not "derived"
const d = new Derived();
```

The order of class initialization, as defined by JavaScript, is:

1. The `base` class fields are initialized
2. The `base` class `constructor` runs
3. The `derived` class fields are initialized
4. The `derived` class `constructor` runs

### **Inheriting Built-in Types**

```tsx
class MsgError extends Error {
  constructor(m: string) {
    super(m);

	// Set the prototype explicitly.
    Object.setPrototypeOf(this, MsgError.prototype);
  }
  sayHello() {
    return "hello " + this.message;
  }
}
```

## Member Visibility

1. `public` can be accessed anywhere
2. `protected` only visible to subclasses of the class they’re declared in
    
    <aside>
    💡 **Exposure of `protected` members**
    
    </aside>
    
    Derived classes need to follow their base class contracts, but may choose to expose a subtype of base class with more capabilities. This includes making `protected` members `public`
    
    ```tsx
    class Base {
      protected m = 10;
    }
    class Derived extends Base {
      // No modifier, so default is 'public'
      m = 15;
    }
    const d = new Derived();
    console.log(d.m); // OK = 15
    ```
    
    ### **Cross-hierarchy `protected` access**
    
    Different OOP languages disagree about whether it’s legal to access a `protected` member through a base class reference
    
    ```tsx
    class Base {
      protected x: number = 1;
    }
    class Derived1 extends Base {
      protected x: number = 5;
    }
    class Derived2 extends Base {
      f1(other: Derived2) {
        other.x = 10;
      }
      f2(other: Base) {
        other.x = 10;
    // Property 'x' is protected and only accessible through an instance
    // of class 'Derived2'. This is an instance of class 'Base'.
      }
    }
    ```
    
    **Java**, for example, considers this to be legal. On the other hand, **C#** and **C++** chose that this code should be illegal.
    
3. `private` like `protected`, but doesn’t allow access to the member even from subclasses
    
    ### **Cross-instance `private` access**
    
    ```tsx
    class A {
      private x = 10;
     
      public sameAs(other: A) {
        // No error
        return other.x === this.x;
      }
    }
    ```
    
    <aside>
    💡 Like other aspects of TypeScript’s type system, private and protected are only enforced during type checking
    
    </aside>
    
    [TS Playground - An online editor for exploring TypeScript and JavaScript](https://www.typescriptlang.org/play?removeComments=true&target=99&ts=4.3.4#code/PTAEGMBsEMGddAEQPYHNQBMCmVoCcsEAHPASwDdoAXLUAM1K0gwQFdZSA7dAKWkoDK4MkSoByBAGJQJLAwAeAWABQIUH0HDSoiTLKUaoUggAW+DHorUsAOlABJcQlhUy4KpACeoLJzrI8cCwMGxU1ABVPIiwhESpMZEJQTmR4lxFQaQxWMm4IZABbIlIYKlJkTlDlXHgkNFAAbxVQTIAjfABrAEEC5FZOeIBeUAAGAG5mmSw8WAroSFIqb2GAIjMiIk8VieVJ8Ar01ncAgAoASkaAXxVr3dUwGoQAYWpMHBgCYn1rekZmNg4eUi0Vi2icoBWJCsNBWoA6WE8AHcAiEwmBgTEtDovtDaMZQLM6PEoQZbA5wSk0q5SO4vD4-AEghZoJwLGYEIRwNBoqAzFRwCZCFUIlFMXECdSiAhId8YZgclx0PsiiVqOVOAAaUAFLAsxWgKiC35MFigfC0FKgSAVVDTSyk+W5dB4fplHVVR6gF7xJrKFotEk-HXIRE9PoDUDDcaTAPTWaceaLZYQlmoPBbHYx-KcQ7HPDnK43FQqfY5+IMDDISPJLCIuqoc47UsuUCofAME3Vzi1r3URvF5QV5A2STtPDdXqunZDgDaYlHnTDrrEAF0dm28B3mDZg6HJwN1+2-hg57ulwNV2NQGoZbjYfNrYiENBwEFaojFiZQK08C-4fFKTVCozWfTgfFgLkeT5AUqiAA)
    
    `private` also allows access using bracket notation during type checking. This makes `private`-declared fields potentially easier to access for things like unit tests, with the drawback that these fields are *soft private* and don’t strictly enforce privacy.
    
    ```tsx
    class MySafe {
      private secretKey = 12345;
    }
     
    const s = new MySafe();
     
    // Not allowed during type checking
    console.log(s.secretKey);
    // Property 'secretKey' is private and only accessible within class 'MySafe'.
     
    // OK
    console.log(s["secretKey"]);
    ```
    
    Unlike TypeScripts’s `private`, JavaScript’s [private fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields) (`#`) remain private after compilation and do not provide the previously mentioned escape hatches like bracket notation access, making them *hard private*.
    
    ```jsx
    class Dog {
      #barkAmount = 0;
      personality = "happy";
     
      constructor() {}
    }
    
    const dog = new Dog()
    dog["#barkAmount"]
    ```
    

## **Static Members**

Classes may have `static` members. These members aren’t associated with a particular instance of the class. They can be accessed through the class constructor object itself

```tsx
class MyClass {
  static x = 0;
  static printX() {
    console.log(MyClass.x);
  }
}
console.log(MyClass.x);
MyClass.printX();
```

<aside>
💡 `Static` members can also use the same `public`, `protected`, and `private` visibility modifiers and are also inherited

</aside>

## `static` Blocks in Classes

Static blocks allow you to write a sequence of statements with their own scope that can access private fields within the containing class.

```tsx
class Foo {
    static #count = 0;
 
    get count() {
        return Foo.#count;
    }
 
    static {
        try {
            const lastInstances = loadLastInstances();
            Foo.#count += lastInstances.length;
        }
        catch {}
    }
```

## **Generic Classes**

```tsx
class Box<Type> {
  contents: Type;
  constructor(value: Type) {
    this.contents = value;
  }
}
 
const b = new Box("hello!"); 
```

### **Type Parameters in Static Members**

This code isn’t legal, and it may not be obvious why:

```tsx
class Box<Type> {
  static defaultValue: Type;
// Static members cannot reference class type parameters.
}
```

Remember that types are always fully erased! At runtime, there’s only *one* `Box.defaultValue` property slot. This means that setting `Box<string>.defaultValue` (if that were possible) would *also* change `Box<number>.defaultValue` - not good. The `static` members of a generic class can never refer to the class’s type parameters.

## `this` at Runtime in Classes

It’s important to remember that **TypeScript** doesn’t change the runtime behavior of **JavaScript**

```tsx
class MyClass {
  name = "MyClass";
  getName() {
    return this.name;
  }
}
const c = new MyClass();
const obj = {
  name: "obj",
  getName: c.getName,
};
 
// Prints "obj", not "MyClass"
console.log(obj.getName());
```

Cause by default, the value of `this` inside a function depends on *how the function was called*

### **Arrow Functions**

```tsx
class MyClass {
  name = "MyClass";
  getName = () => {
    return this.name;
  };
}
const c = new MyClass();
const g = c.getName;
// Prints "MyClass" instead of crashing
console.log(g());
```

This has some trade-offs:

- The `this` value is guaranteed to be correct at runtime, even for code not checked with TypeScript
- This will use more memory, because each class instance will have its own copy of each function defined this way
- You can’t use `super.getName` in a derived class, because there’s no entry in the prototype chain to fetch the base class method from

### `this` parameters

In a method or function definition, an initial parameter named `this` has special meaning in TypeScript. These parameters are erased during compilation

```tsx
// TypeScript input with 'this' parameter
function fn(this: SomeType, x: number) {
  /* ... */
}
```

TypeScript checks that calling a function with a `this` parameter is done so with a correct context. Instead of using an arrow function, we can add a `this` parameter to method definitions to statically enforce that the method is called correctly

```tsx
class MyClass {
  name = "MyClass";
  getName(this: MyClass) {
    return this.name;
  }
}
const c = new MyClass();
// OK
c.getName();
 
// Error, would crash
const g = c.getName;
console.log(g());
// The 'this' context of type 'void' is
// not assignable to method's 'this' of type 'MyClass'.
```

## `this` Types

In classes, a special type called `this` refers *dynamically* to the type of the current class

```tsx
class Box {
  contents: string = "";
  set(value: string) {
    this.contents = value;
    return this;
  }
}
```

Here, TypeScript inferred the return type of `set` to be `this`, rather than `Box`

```tsx
class ClearableBox extends Box {
  clear() {
    this.contents = "";
  }
}
 
const a = new ClearableBox();
const b = a.set("hello"); 
		// const b: ClearableBox
```

We can also use `this` in a parameter type annotation

```tsx
class Box {
  content: string = "";
  sameAs(other: this) {
    return other.content === this.content;
  }
}
```

This is different from writing `other: Box` — if you have a derived class, its `sameAs` method will now only accept other instances of that same derived class

```tsx
class DerivedBox extends Box {
  otherContent: string = "?";
}
 
const base = new Box();
const derived = new DerivedBox();
derived.sameAs(base);
// Argument of type 'Box' is not assignable to parameter of type 'DerivedBox'.
// Property 'otherContent' is missing in type 'Box' but required in type 'DerivedBox'.
```

### `this` based type guards

We can use `this is Type` in the return position for methods in classes and interfaces.

```tsx
class FileSystemObject {
  isFile(): this is FileRep {
    return this instanceof FileRep;
  }
  isDirectory(): this is Directory {
    return this instanceof Directory;
  }
  isNetworked(): this is Networked & this {
    return this.networked;
  }
  constructor(public path: string, private networked: boolean) {}
}
 
class FileRep extends FileSystemObject {
  constructor(path: string, public content: string) {
    super(path, false);
  }
}

class Directory extends FileSystemObject {
  children: FileSystemObject[];
}
 
interface Networked {
  host: string;
}

const fso: FileSystemObject = new FileRep("foo/bar.txt", "foo");
 
if (fso.isFile()) {
  fso.content;
  // const fso: FileRep
} else if (fso.isDirectory()) {
  fso.children;
  // const fso: Directory
} else if (fso.isNetworked()) {
  fso.host;
  // const fso: Networked & FileSystemObject
}
```

A common use-case for a this-based type guard is to allow for lazy validation of a particular field. For example, this case removes an `undefined` from the value held inside box when `hasValue` has been verified to be true

```tsx
class Box<T> {
  value?: T;
 
  hasValue(): this is { value: T } {
    return this.value !== undefined;
  }
}
 
const box = new Box();
box.value = "Gameboy";
 
box.value;
     // (property) Box<unknown>.value?: unknown
 
if (box.hasValue()) {
  box.value;
       // (property) value: unknown
}
```

## **Parameter Properties**

`public`, `private`, `protected`, or `readonly`.

## `abstract` Classes and Members

An *abstract method* or *abstract field* is one that hasn’t had an implementation provided. These members must exist inside an *abstract class*, which cannot be directly instantiated.

```tsx
abstract class Base {
  abstract getName(): string; // abstract member
 
  printName() {
    console.log("Hello, " + this.getName());
  }
}
 
const b = new Base();
// Cannot create an instance of an abstract class.
```

We can’t instantiate `Base` with `new` because it’s abstract. Instead, we need to make a derived class and implement the abstract members

```tsx
class Derived extends Base {
  getName() {
    return "world";
  }
}
 
const d = new Derived();
d.printName();
```

## **Relationships Between Classes**

In most cases, classes in TypeScript are compared structurally, the same as other types.

```tsx
class Point1 {
  x = 0;
  y = 0;
}
 
class Point2 {
  x = 0;
  y = 0;
}
 
// OK
const p: Point1 = new Point2();
```

Similarly, subtype relationships between classes exist even if there’s no explicit inheritance

```tsx
class Person {
  name: string;
  age: number;
}
 
class Employee {
  name: string;
  age: number;
  salary: number;
}
 
// OK
const p: Person = new Employee();
```