---
Created: 2025-06-21T16:45:00
tags:
  - Learning
  - Java
Type: Backend
Materials:
  - https://www.youtube.com/watch?v=xk4_1vDrzzo 
  - "[[Java Learning Plan]]"
---
# What is Java
Java is high-level, class-based, object-oriented programming language.

> [!INFO] WORA
> The language was developed with the "*Write Once, Run Anywhere*" philosophy.

It borrows its syntax from ==*C*== and ==*C++*==, but eliminates certain low-level programming complexities.
Unlike these two languages, ***Java*** does not require you to manually clean the application memory, as it has a garbage collector that performs this task automatically. Known for its robustness, security, and simplicity, Java has become a popular choice among developers worldwide.
## A sample of Java
Hello world!
```java
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello world!");
	}
}
```

- `public class HelloWorld` - In **Java**, all the code you write will be inside classes. Every Java application has to have at least one class.
- `public static void main(String[] args)` - This is the heart of the program, where the execution begins.
# Basic literals
Regardless of its complexity, a program always performs operations on numbers, strings, and other values. These values are called ==**literals**==.
![[Pasted image 20250628104102.png|400]]