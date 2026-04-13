Enums are one of the few features ==**[[TypeScript]]**== has which is not a type-level extension of **==[[JavaScript]]==**.

  

## **Numeric enums**

An enum can be defined using the `enum` keyword.

```TypeScript
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}
```

Above, we have a numeric enum where `Up` is initialized with `1`. All of the following members are auto-incremented from that point on. In other words, `Direction.Up` has the value `1`, `Down` has `2`, `Left` has `3`, and `Right` has `4`.

  

## String enums

String enums are a similar concept, but have some subtle [runtime differences](https://www.typescriptlang.org/docs/handbook/enums.html#enums-at-runtime).

In a string enum, each member has to be constant-initialized with a string literal, or with another string enum member.

```TypeScript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```

While string enums don’t have auto-incrementing behavior, string enums have the benefit that they “serialize” well.

  

## **Heterogeneous enums**

> [!important] Technically enums can be mixed with string and numeric members, but it’s not clear why you would ever want to do so

```TypeScript
enum BooleanLikeHeterogeneousEnum {
  No = 0,
  Yes = "YES",
}
```

  

## **Computed and constant members**

Each enum member has a value associated with it which can be either ==_constant_== or ==_computed_==.

- It is the first member in the enum and it has no initializer, in which case it’s assigned the value `0`
    
    ```TypeScript
    // E.X is constant:
    enum E {
      X,
    }
    ```
    
- It does not have an initializer and the preceding enum member was a _numeric_ constant
    
    ```TypeScript
    // All enum members in 'E1' and 'E2' are constant.
     
    enum E1 {
      X, //0
      Y, //1
      Z, //2
    }
     
    enum E2 {
      A = 1,
      B, //2
      C, //3
    }
    ```
    
- The enum member is initialized with a constant enum expression. A constant enum expression is a subset of ==**TypeScript**== expressions that can be fully evaluated at compile time. An expression is a constant enum expression if it is
    
    1. a literal enum expression (basically a string literal or a numeric literal)
    2. a reference to previously defined constant enum member (which can originate from a different enum)
    3. a parenthesized constant enum expression
    4. one of the `+`, , `~` unary operators applied to constant enum expression
    5. `+`, , , `/`, `%`, `<<`, `>>`, `>>>`, `&`, `|`, `^` binary operators with constant enum expressions as operands
    
    It is a compile time error for constant enum expressions to be evaluated to `NaN` or `Infinity`.
    

  

In all other cases enum member is considered computed

```TypeScript
enum FileAccess {
  // constant members
  None,
  Read = 1 << 1,
  Write = 1 << 2,
  ReadWrite = Read | Write,

  // computed member
  G = "123".length,
}
```

  

## **Union enums and enum member types**

There is a special subset of constant enum members that aren’t calculated: literal enum members.

> [!important] When all members in an enum have literal enum values, some special semantics come into play.

  

The first is that enum members also become types as well

```TypeScript
enum ShapeKind {
  Circle,
  Square,
}
 
interface Circle {
  kind: ShapeKind.Circle;
  radius: number;
}
 
interface Square {
  kind: ShapeKind.Square;
  sideLength: number;
}
 
let c: Circle = {
  kind: ShapeKind.Square,
// Type 'ShapeKind.Square' is not assignable to type 'ShapeKind.Circle'.
  radius: 100,
};
```

  

## **Enums at runtime**

> [!important] Enums are real objects that exist at runtime.

  

```TypeScript
enum E {
  X,
  Y,
  Z,
}
 
function f(obj: { X: number }) {
  return obj.X;
}
 
// Works, since 'E' has a property named 'X' which is a number.
f(E); //0
```

  

## **Enums at compile time**

Even though Enums are real objects that exist at runtime, the `keyof` keyword works differently than you might expect for typical objects. Instead, use `keyof typeof` to get a Type that represents all Enum keys as strings.

```TypeScript
enum LogLevel {
  ERROR,
  WARN,
  INFO,
  DEBUG,
}
 
/**
 * This is equivalent to:
 * type LogLevelStrings = 'ERROR' | 'WARN' | 'INFO' | 'DEBUG';
 */
type LogLevelStrings = keyof typeof LogLevel;
```

  

### **Reverse mappings**

In addition to creating an object with property names for members, numeric enums members also get a ==_reverse mapping_== from enum values to enum names

```TypeScript
enum Enum {
  A,
}
 
let a = Enum.A;
let nameOfA = Enum[a]; // "A"
```

  

### `const` enums

In most cases, enums are a perfectly valid solution. However sometimes requirements are tighter. To avoid paying the cost of extra generated code and additional indirection when accessing enum values, it’s possible to use `const` enums.

```TypeScript
const enum Enum {
  A = 1,
  B = A * 2,
}
```

  

==Const enums== can only use constant enum expressions and unlike regular enums they are completely removed during compilation. Const enum members are ==inlined== at use sites. This is possible since const enums cannot have computed members.

```TypeScript
const enum Direction {
  Up,
  Down,
  Left,
  Right,
}
 
let directions = [
  Direction.Up,
  Direction.Down,
  Direction.Left,
  Direction.Right,
];
```

  

## **Ambient enums**

Ambient enums are used to describe the shape of already existing enum types.

```TypeScript
declare enum Enum {
  A = 1,
  B,
  C = 2,
}
```

  

## Objects vs Enums

In modern ==**TypeScript**==, you may not need an enum when an object with `as const` could suffice

```TypeScript
const enum EDirection {
  Up,
  Down,
  Left,
  Right,
}
 
const ODirection = {
  Up: 0,
  Down: 1,
  Left: 2,
  Right: 3,
} as const;
 
EDirection.Up;
           // (enum member) EDirection.Up = 0
 
ODirection.Up;
           // (property) Up: 0
```

## Related
- [[TypeScript]]
- [[JavaScript]]
- [[Narrowing]]