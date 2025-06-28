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
![[Pasted image 20250628104102.png#center|400]]
### Integer numbers
```java
int numApples = 1000;
```
We can increase code readability by dividing the digit into blocks with underscores: `1_000_000` is more readable than `1000000`.
```java
int numPackedApples = 1_000_000;
```
### Characters
A character is a single symbol, denoted with ==single quotes==.
```java
char charOne = '1';
int numOne = 1;
```
### Strings
A string is a sequence of characters, encapsulated by ==double quotes==.
A string consisting of a single character like `"A"` is also a valid string, but do not confuse it with the `'A'` character. Note the difference in quotes!
```java
char singleQuoted = 'A';
String doubleQuoted = "A";
```
# Writing first Java program
## Basic
- The `public class`, it is the basic unit of a program. Every Java program must have at least one class. The definition of a class consists of the `class` keyword followed by the class name.
- The ==main== method, to make the program ==runnable==, we put a method named `main` inside a class, otherwise, it will not run.
![[Data types and variables]]