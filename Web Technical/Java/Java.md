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
## Data type and variable
```java
// structure
DataType variableName = initialization;

String language = "java";

int numberOfApples = 5;
```
### Alternative form of declaring
```java
String language = "java", version = "8 or newer";
```
Creating 2 `String` variables.
### Type inference
Since **Java 10**, we can use `var` instead of a specific type to enforce type inference
```java
// structure
var variableName = initialization;

var language = "Java"; // String
var version = 10; // int
```
## Java documentation comment
The compiler ignores any text from `/**` to `*/` just like it ignores multi-line comments.
These kinds of comments can be used to automatically generate documentation about your source code by using the **[javadoc](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html)** tool.
```java
public class HelloWorld {
/**
* The main method is the entry point of the Java application.
* It prints "Hello, World!" and a simple message to the console.
*
* @param args command line arguments (not used in this program)
*/
	public static void main(String[] args) {
		System.out.println("Hello, World!");
		System.out.println("This is a simple Java program.");
	}
}
```
## Reading input
The simplest method to obtain data from the standard input is using the standard class `Scanner`. It allows a program to read values of various types, like strings or numbers, from the standard input.
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        sc.close();
    }
}
```
Set up the `Scanner` class and telling it to listen for answers from the keyboard (which is represented by `System.in`).

> [!note] Using `Scanner`
> When you use a `Scanner` in **Java**, it’s like opening a notebook to take notes or read from it. When you’re done using the notebook, you `.close()` it to keep things tidy and make sure it’s properly put away.

We can also read others data type.
```java
class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        double b = sc.nextDouble();
        boolean c = sc.nextBoolean();
        
        sc.close();
    }
}
```
### Character Encoding in Scanner
Starting with **Java 18**, the default character encoding used by `Scanner` and other Java APIs is `UTF-8`.

Previously, **Java** relied on the platform’s default charset, which varied depending on the system locale and operating system (e.g., Windows might use `Cp1252`, Linux might use `UTF-8`, etc.).

This inconsistency often led to subtle bugs, especially when handling special characters, accented letters, or non-Latin alphabets. `UTF-8` ensures that characters like `é`, `ö`, or `你好` are read and interpreted correctly across all platforms.

> [!NOTE] 
> Keep in mind that programs running on older **Java** versions (before 18) might behave differently depending on the environment.

