# Introduce

At its core, a **decorator is just a function** that is applied to a **class**, **method**, **property**, or **parameter** at design time (i.e., during definition, not at runtime execution).

It’s syntactic sugar for attaching **metadata** or **enhancing behavior**.

> [!important] Think of it like a wrapper or a modifier that adds extra logic to whatever it decorates.

```TypeScript
// [[TypeScript]] decorator example
function Logger(constructor: Function) {
  console.log("Class created:", constructor.name);
}

@Logger
class MyService {}
```

When the file (code above) is parsed, the decorator `@Logger` is called **with the constructor function of the class**.

So in essence, it’s just this:

```TypeScript
Logger(MyService);
```

## Different types of decorator

|Type|Signature|
|---|---|
|**Class**|`(constructor: Function)`|
|**Property**|`(target: any, propertyKey: string)`|
|**Method**|`(target: any, propertyKey: string, descriptor: PropertyDescriptor)`|
|**Parameter**|`(target: any, propertyKey: string, parameterIndex: number)`|

# Decorator logic usages

## Add metadata

Using `Reflect-metadata` or custom logic to attach data to class.

```TypeScript
import 'reflect-metadata';

function CustomMeta(data: string) {
  return Reflect.metadata('custom:data', data);
}

@CustomMeta('hello')
class Example {}

console.log(Reflect.getMetadata('custom:data', Example)); // "hello"
```

Frameworks like **[[NestJS]]** use this kind of technique to:

- Know what services to inject
- Enforce guards/roles
- Parse request body types

## Wrap or replace logic

```TypeScript
function Log() {
  return function (target, key, descriptor) {
    const original = descriptor.value;
    descriptor.value = function (...args) {
      console.log(`Called ${key} with`, args);
      return original.apply(this, args);
    };
  };
}

class MathService {
  @Log()
  add(a: number, b: number) {
    return a + b;
  }
}
```

So when we call `add(2,3)`

```TypeScript
Call add with [2, 3]
```

  

# 🧠 Final Summary: The Logic Behind Decorators

- A **decorator is a function that gets applied to a class/member when it's defined**.
- It can **add, modify, or replace behavior**, or **attach metadata** to elements.
- **NestJS** and others build on this to create elegant patterns for DI, routing, auth, etc.
- Under the hood, it's just **JavaScript functions working with objects, functions, and metadata**.

## Related

- [[NestJS]]
- [[TypeScript]]