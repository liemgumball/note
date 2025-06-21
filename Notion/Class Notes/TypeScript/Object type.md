## In **==JavaScript==**, the fundamental way that we group and pass around data is through objects. In ==**TypeScript**==, we represent those through ==_object types_==.

```TypeScript
function greet(person: { name: string; age: number }) {
  return "Hello " + person.name;
}
```

They can be named by using either an ==_interface_== _or a_ ==_type alias_==

```TypeScript
interface Person {
  name: string;
  age: number;
}

type Person = {
  name: string;
  age: number;
}
```

  

## Properties

In JavaScript, even if the property has never been set, we can still access it - it’s just going to give us the value `undefined`. We can just handle `undefined` specially by checking for it.

  

## `readonly` Properties

```TypeScript
interface SomeType {
  readonly prop: string;
}
 
function doSomething(obj: SomeType) {
  // We can read from 'obj.prop'.
  console.log(`prop has the value '${obj.prop}'.`);
 
  // But we can't re-assign it.
  obj.prop = "hello";
// Cannot assign to 'prop' because it is a read-only property.
}
```

  

> [!important] Using the 
> 
> `readonly` modifier doesn’t necessarily imply that a value is totally immutable - or in other words, that its internal contents can’t be changed. It just means the property itself can’t be re-written to.

```TypeScript
interface Person {
  name: string;
  age: number;
}
 
interface ReadonlyPerson {
  readonly name: string;
  readonly age: number;
}
 
let writablePerson: Person = {
  name: "Person McPersonface",
  age: 42,
};
 
// works
let readonlyPerson: ReadonlyPerson = writablePerson;
 
console.log(readonlyPerson.age); // prints '42'
writablePerson.age++;
console.log(readonlyPerson.age); // prints '43'
```

  

## **Index Signatures**

```TypeScript
interface ReadonlyStringArray {
  readonly [index: number]: string;
 
  name: string; // ok
  lenght: number;
// Property 'lenght' of type 'number' is not assignable to 'number' index type 'string'.
}

let myArray: ReadonlyStringArray = getReadOnlyStringArray();
myArray[2] = "Mallory";
// Index signature in type 'ReadonlyStringArray' only permits reading.
```

  

## **Excess Property Checks**

```TypeScript
interface SquareConfig {
  color?: string;
  width?: number;
}

let mySquare = createSquare({ colour: "red", width: 100 });
// Argument of type '{ colour: string; width: number; }' is not assignable to
// parameter of type 'SquareConfig'.
//  Object literal may only specify known properties, but
// 'colour' does not exist in type 'SquareConfig'. Did you mean to write 'color'?
```

The given argument to `createSquare` is spelled `_colour_` instead of `color`. In plain **==JavaScript==**, this sort of thing fails silently.

However, ==**TypeScript**== takes the stance that there’s probably a ==bug== in this code. Object literals get special treatment and undergo _excess property checking_ when assigning them to other variables, or passing them as arguments. If an object literal has any properties that the “target type” doesn’t have, you’ll get an ==error==

  

Getting around these checks is actually really simple. The easiest method is to just use a type assertion:

```TypeScript
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
```

  

However, a better approach might be to add a ==string index signature== if we’re sure that the object can have some extra properties that are used in some special way.

```TypeScript
interface SquareConfig {
  color?: string;
  width?: number;
  [propName: string]: any;
}
```

  

## **Extending Types**

```TypeScript
interface Colorful {
  color: string;
}
 
interface Circle {
  radius: number;
}
 
interface ColorfulCircle extends Colorful, Circle {}
 
const cc: ColorfulCircle = {
  color: "red",
  radius: 42,
};
```

  

## **Intersection Types**

`interface` allowed us to build up new types from other types by extending them. ==**TypeScript**== provides another construct called ==_intersection types_== that is mainly used to combine existing object types.

```TypeScript
interface Colorful {
  color: string;
}
interface Circle {
  radius: number;
}
 
type ColorfulCircle = Colorful & Circle;
```

  

## Generic `object` Types

```TypeScript
interface Box<Type> {
  contents: Type;
}
 
interface Apple {
  // ....
}
 
// Same as '{ contents: Apple }'.
type AppleBox = Box<Apple>;
```

## The `Array` Type

Much like the `Box` type above, `Array` itself is a generic type.

```TypeScript
interface Array<Type> {
  /**
   * Gets or sets the length of the array.
   */
  length: number;
 
  /**
   * Removes the last element from an array and returns it.
   */
  pop(): Type | undefined;
 
  /**
   * Appends new elements to an array, and returns the new length of the array.
   */
  push(...items: Type[]): number;
 
  // ...
}
```

> [!important] ==**TypeScript**==
> 
> provides a shorthand syntax for `Array<Type>` with `Type[]`

  

## The `ReadonlyArray` Type

```TypeScript
function doStuff(values: ReadonlyArray<string>) {
  // We can read from 'values'...
  const copy = values.slice();
  console.log(`The first value is ${values[0]}`);
 
  // ...but we can't mutate 'values'.
  values.push("hello!");
Property 'push' does not exist on type 'readonly string[]'.
}
```

  

Unlike `Array`, there isn’t a `ReadonlyArray` constructor that we can use.

```TypeScript
new ReadonlyArray("red", "green", "blue");
//'ReadonlyArray' only refers to a type, but is being used as a value here.
```

Instead, we can assign regular `Array`s to `ReadonlyArray`

```TypeScript
const roArray: ReadonlyArray<string> = ["red", "green", "blue"];
```

  

> [!important] Just as
> 
> ==**TypeScript**== provides a shorthand syntax for `Array<Type>` with `Type[]`, it also provides a shorthand syntax for `ReadonlyArray<Type>` with `readonly Type[]`.

  

## **Tuple Types**

A ==_tuple type_== is another sort of `Array` type that knows exactly how many elements it contains, and exactly which types it contains at specific positions.

```TypeScript
type StringNumberPair = [string, number];

function doSomething(pair: StringNumberPair) {
  const a = pair[0];
       //const a: string
  const b = pair[1];
       //const b: number
}
```

  

Tuples can also have rest elements, which have to be an array/tuple type.

```TypeScript
type StringNumberBooleans = [string, number, ...boolean[]];
type StringBooleansNumber = [string, ...boolean[], number];
type BooleansStringNumber = [...boolean[], string, number];
```

  

==Tuples== tend to be created and left un-modified in most code, so annotating types as `readonly` tuples when possible is a good default. This is also important given that array literals with `const` assertions will be inferred with `readonly` tuple types.

```TypeScript
let point = [3, 4] as const;
 
function distanceFromOrigin([x, y]: [number, number]) {
  return Math.sqrt(x ** 2 + y ** 2);
}
 
distanceFromOrigin(point);
```