## `Awaited<Type>`

This type is meant to model operations like `await` in `async` functions, or the `.then()` method on `Promise`

```tsx
type A = Awaited<Promise<string>>;
    // type A = string
 
type B = Awaited<Promise<Promise<number>>>;
    // type B = number
 
type C = Awaited<boolean | Promise<number>>;
    // type C = number | boolean
```

## **`Partial<Type>`**

Constructs a type with all properties of `Type` set to optional. This utility will return a type that represents all subsets of a given type.

```tsx
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
  title: "organize desk",
  description: "clear clutter",
};

const todo2 = updateTodo(todo1, {
  description: "throw out trash",
});
```

## **`Required<Type>`**

Constructs a type consisting of all properties of `Type` set to required. The opposite of [`Partial`](Utility%20Types.md)

```tsx
interface Props {
  a?: number;
  b?: string;
}
 
const obj: Props = { a: 5 };
 
const obj2: Required<Props> = { a: 5 };
// Property 'b' is missing in type '{ a: number; }'
// but required in type
```

## **`Readonly<Type>`**

```tsx
interface Todo {
  title: string;
}
 
const todo: Readonly<Todo> = {
  title: "Delete inactive users",
};
 
todo.title = "Hello";
// Cannot assign to 'title' because it is a read-only property.
```

## **`Record<Keys, Type>`**

Constructs an object type whose property keys are `Keys` and whose property values are `Type`. This utility can be used to map the properties of a type to another type.

```tsx
interface CatInfo {
  age: number;
  breed: string;
}
 
type CatName = "miffy" | "boris" | "mordred";
 
const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: "Persian" },
  boris: { age: 5, breed: "Maine Coon" },
  mordred: { age: 16, breed: "British Shorthair" },
};
 
cats.boris;
 // const cats: Record<CatName, CatInfo>
```

## **`Pick<Type, Keys>`**

Constructs a type by picking the set of properties `Keys` (string literal or union of string literals) from `Type`

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}
 
type TodoPreview = Pick<Todo, "title" | "completed">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
 
todo;
 // const todo: TodoPreview
```

## **`Omit<Type, Keys>`**

Constructs a type by picking all properties from `Type` and then removing `Keys` (string literal or union of string literals). The opposite of [`Pick`](Utility%20Types.md).

```tsx
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}
 
type TodoPreview = Omit<Todo, "description">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
  createdAt: 1615544252770,
};
 
todo;
 // const todo: TodoPreview
 
type TodoInfo = Omit<Todo, "completed" | "createdAt">;
 
const todoInfo: TodoInfo = {
  title: "Pick up kids",
  description: "Kindergarten closes at 5pm",
};
 
todoInfo;
   // const todoInfo: TodoInfo
```

## **`Exclude<UnionType, ExcludedMembers>`**

Constructs a type by excluding from `UnionType` all union members that are assignable to `ExcludedMembers`

```tsx
type T0 = Exclude<"a" | "b" | "c", "a">;
     // type T0 = "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">;
     // type T1 = "c"
type T2 = Exclude<string | number | (() => void), Function>;
     // type T2 = string | number
```

## **`NonNullable<Type>`**

```tsx
type T0 = NonNullable<string | number | undefined>;
     // type T0 = string | number
type T1 = NonNullable<string[] | null | undefined>;
     // type T1 = string[]
```

## **`Parameters<Type>`**

Constructs a tuple type from the types used in the parameters of a function type `Type`

```tsx
declare function f1(arg: { a: number; b: string }): void;
 
type T0 = Parameters<() => string>;
     // type T0 = []
type T1 = Parameters<(s: string) => void>;
     // type T1 = [s: string]
type T2 = Parameters<<T>(arg: T) => T>;
     // type T2 = [arg: unknown]
type T3 = Parameters<typeof f1>;
     // type T3 = [arg: { a: number; b: string; }]
```

## **`ConstructorParameters<Type>`**

Constructs a tuple or array type from the types of a constructor function type. It produces a tuple type with all the parameter types (or the type `never` if `Type` is not a function).

```tsx
type T0 = ConstructorParameters<ErrorConstructor>;
     // type T0 = [message?: string]
type T1 = ConstructorParameters<FunctionConstructor>;
     // type T1 = string[]
```

## **`ReturnType<Type>`**

Constructs a type consisting of the return type of function `Type`

```tsx
type T0 = ReturnType<() => string>;
     // type T0 = string
type T1 = ReturnType<(s: string) => void>;
     // type T1 = void
type T2 = ReturnType<<T>() => T>;
     // type T2 = unknown
```

## **`InstanceType<Type>`**

Constructs a type consisting of the instance type of a constructor function in `Type`

```tsx
class C {
  x = 0;
  y = 0;
}
 
type T0 = InstanceType<typeof C>;
     // type T0 = C
type T1 = InstanceType<any>;
     // type T1 = any
type T2 = InstanceType<never>;
     // type T2 = never
```

## **`ThisParameterType<Type>`**

Extracts the type of the [this](https://www.typescriptlang.org/docs/handbook/functions.html#this-parameters) parameter for a function type, or [unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type) if the function type has no `this` parameter.

```tsx
function toHex(this: Number) {
  return this.toString(16);
}
 
function numberToString(n: ThisParameterType<typeof toHex>) {
  return toHex.apply(n);
}
```

## **`OmitThisParameter<Type>`**

Removes the [`this`](https://www.typescriptlang.org/docs/handbook/functions.html#this-parameters) parameter from `Type`. If `Type` has no explicitly declared `this` parameter, the result is simply `Type`. Otherwise, a new function type with no `this` parameter is created from `Type`. Generics are erased and only the last overload signature is propagated into the new function type.

```tsx
function toHex(this: Number) {
  return this.toString(16);
}
 
const fiveToHex: OmitThisParameter<typeof toHex> = toHex.bind(5);
 
console.log(fiveToHex());
```

## **`ThisType<Type>`**

This utility does not return a transformed type. Instead, it serves as a marker for a contextual [`this`](https://www.typescriptlang.org/docs/handbook/functions.html#this) type. Note that the [`noImplicitThis`](https://www.typescriptlang.org/tsconfig#noImplicitThis) flag must be enabled to use this utility.

```tsx
type ObjectDescriptor<D, M> = {
  data?: D;
  methods?: M & ThisType<D & M>; // Type of 'this' in methods is D & M
};
 
function makeObject<D, M>(desc: ObjectDescriptor<D, M>): D & M {
  let data: object = desc.data || {};
  let methods: object = desc.methods || {};
  return { ...data, ...methods } as D & M;
}
 
let obj = makeObject({
  data: { x: 0, y: 0 },
  methods: {
    moveBy(dx: number, dy: number) {
      this.x += dx; // Strongly typed this
      this.y += dy; // Strongly typed this
    },
  },
});
 
obj.x = 10;
obj.y = 20;
obj.moveBy(5, 5);
```

## Intrinsic String Manipulation Types

- `Uppercase<StringType>`
- `Lowercase<StringType>`
- `Capitalize<StringType>`
- `Uncapitalize<StringType>`