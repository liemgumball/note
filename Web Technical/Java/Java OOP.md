# The core of [[Java]]
**Object-oriented programming** is about creating objects that contain both data and methods.
**OOP** has several advantages over procedural programming:
- **OOP** is faster and easier to execute
- **OOP** provides a clear structure for the programs
- **OOP** helps to keep the Java code DRY "Don't Repeat Yourself", and makes the code easier to maintain, modify and debug
- **OOP** makes it possible to create full reusable applications with less code and shorter development time
# Class and Object

| Class | Object               |
| ----- | -------------------- |
| Fruit | Apple, Orange, Mango |
| Car   | BMW, Honda, Volvo    |
```java
public class Fruit {
	public String say() {
		return "I'm a Fruit";	
	}
}

Fruit apple = new Fruit();
Fruit orange = new Fruit();
```
## Static vs Public
You will often see Java programs that have either `static` or `public` attributes and methods.

In the example above, we created a `static` method, which means that it ==can be accessed without creating an object== of the class, unlike `public`, which can only be accessed by objects.
## ## Keyword `this`

The `this` keyword in **Java** refers to the current object in a method or constructor.
### Calling a Constructor from Another Constructor

You can also use `this()` to call another constructor in the same class.

This is useful when you want to provide default values or reuse initialization code instead of repeating it.

## Related

- [[Java]]