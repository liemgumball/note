[[TypeScript]] provides several ways to narrow types within conditional blocks.

## Take this example

```TypeScript
function padLeft(padding: number | string, input: string) {
  return " ".repeat(padding) + input;
// Argument of type 'string | number' is not assignable to parameter of type 'number'.
// Type 'string' is not assignable to type 'number'.
}
```

If `padding` is a `number`, it will treat that as the number of spaces we want to prepend to `input`. If `padding` is a `string`, it should just prepend `padding` to `input`

  

==TypeScript== is warning us that we’re passing a value with type `number | string` to the `repeat` function, which only accepts a `number`

```TypeScript
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

  

## `typeof` type guards

As we’ve seen, JavaScript supports a `typeof` operator which can give very basic information about the type of values we have at runtime. TypeScript expects this to return a certain set of strings:

- `"string"`
- `"number"`
- `"bigint"`
- `"boolean"`
- `"symbol"`
- `"undefined"`
- `"object"`
- `"function"`

  

## **Truthiness narrowing**

In ==JavaScript==, we can use any expression in conditionals, `&&`, `||`, `if` statements, Boolean negations (`!`), and more.

```TypeScript
function getUsersOnlineMessage(numUsersOnline: number) {
  if (numUsersOnline) {
    return `There are ${numUsersOnline} online now!`;
  }
  return "Nobody's here. :(";
}
```

In example, `if` statements don’t expect their condition to always have the type `boolean`.

  

In ==JavaScript==, constructs like `if` first “coerce” their conditions to `boolean`s to make sense of them, and then choose their branches depending on whether the result is `true` or `false`

- `0`
- `NaN`
- `""` (the empty string)
- `0n` (the `bigint` version of zero)
- `null`
- `undefined`

all coerce to `false`, and other values get coerced to `true`

  

```TypeScript
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    for (const s of strs) {
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  }
}
```

We wrapped the entire body of the function in a truthy check, but this has a subtle downside: we may no longer be handling the ==empty string== case correctly.

  

## **Equality narrowing**

TypeScript also uses `switch` statements and equality checks like `===`, `!==`, `==`, and `!=` to narrow types.

  

JavaScript’s looser equality checks with `==` and `!=` also get narrowed correctly. Checking whether something `== null` actually not only checks whether it is specifically the value `null` - it also checks whether it’s potentially `undefined`

  

Example:

```TypeScript
function multiplyValue(value: number | null | undefined, factor: number) {
  // Remove both 'null' from the type.
  if (value !== null) {
    console.log(value);
		//the result can be "undefined"
  }
}
```

and

```TypeScript
function multiplyValue(value: number | null | undefined, factor: number) {
  // Remove both 'null' and 'undefined' from the type.
  if (value != null) {
    console.log(value);
  }
}
```

  

## The `in` operator narrowing

```TypeScript
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };
 
function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    return animal.swim();
								// Fish | Human
  }
  return animal.fly();
								// Bird | Human
}
```

  

## `instanceof` narrowing

```TypeScript
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString());
							// Date
  } else {
    console.log(x.toUpperCase());
							// srting
  }
```

  

## **Nullish Coalescing with** `**??**`

```TypeScript
let value = getValue() ?? "Default";

# equal to
let value = getValue()
if(!value) value = "Default";
```

  

## **Using type** ==**predicates**==

To define a user-defined type guard, we simply need to define a function whose return type is a _type predicate_

```TypeScript

type Fish = { swim: () => void };
type Bird = { fly: () => void };
declare function getSmallPet(): Fish | Bird;
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
// Both calls to 'swim' and 'fly' are now okay.
let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

`pet is Fish` is our type predicate in this example. A predicate takes the form `parameterName is Type`, where `parameterName` must be the name of a parameter from the current function signature.

Any time `isFish` is called with some variable, TypeScript will _narrow_ that variable to that specific type if the original type is compatible.

In addition, classes can use `this is Type` to narrow their type.

> [!info] Documentation - Classes  
> How classes work in TypeScript  
> [https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards)  

  

## **Assertion functions**

Types can also be narrowed using **==Assertion functions==**

> [!info] Documentation - TypeScript 3.7  
> TypeScript 3.  
> [https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions)  

```TypeScript
function multiply(x, y) {
  assert(typeof x === "number");
  assert(typeof y === "number");
  return x * y;
}
```

  

## **Discriminated unions**

Most of the examples we’ve looked at so far have focused around narrowing single variables with simple types like `string`, `boolean`, and `number`. While this is common, most of the time in JavaScript we’ll be dealing with slightly more complex structures

```TypeScript
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}
```

  

We can write a `getArea` function that applies the right logic based on if it’s dealing with a circle or square. We’ll first try dealing with circles.

```TypeScript
function getArea(shape: Shape) {
  return Math.PI * shape.radius ** 2;
// 'shape.radius' is possibly 'undefined'.
}
```

  

The JavaScript still doesn’t work even we perform the appropriate checks on the `kind` property

```TypeScript
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
// 'shape.radius' is possibly 'undefined'.
  }
}
```

  

We’ve hit a point where we know more about our values than the type checker does. We could try to use a non-null assertion (a `!` after `shape.radius`) to say that `radius` is **==definitely==** present.

```TypeScript
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius! ** 2;
  }
}
```

  

> [!important] The problem with this encoding of 
> 
> `Shape` is that the type-checker doesn’t have any way to know whether or not `radius` or `sideLength` are present based on the `kind` property.

  

We should write like this:

```TypeScript
interface Circle {
  kind: "circle";
  radius: number;
}
 
interface Square {
  kind: "square";
  sideLength: number;
}
 
type Shape = Circle | Square;
```

  

## The `never` type

When narrowing, you can reduce the options of a union to a point where you have removed all possibilities and have nothing left. In those cases, ==**TypeScript**== will use a `never` type to represent a state which ==shouldn’t exist==.

### **Exhaustiveness checking**

The `never` type is assignable to every type; however, no type is assignable to `never` (except `never` itself). This means you can use narrowing and rely on `never` turning up to do exhaustive checking in a `switch` statement.

```TypeScript
type Shape = Circle | Square;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```

  

Adding a new member to the `Shape` union, will cause a TypeScript error:

```TypeScript
interface Triangle {
  kind: "triangle";
  sideLength: number;
}
 
type Shape = Circle | Square | Triangle;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
// Type 'Triangle' is not assignable to type 'never'.
      return _exhaustiveCheck;
  }
}
```

## Related
- [[TypeScript]]
- [[More on function]]
- [[Object type]]