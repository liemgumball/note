---
Created: 2024-02-15T15:46
Class: Agility IO InternShip
Type: Back-end
Materials:
  - https://www.w3schools.com/nodejs
  - https://nodejs.org/api/
Reviewed: false
Edited: 2025-05-10T14:46
---
# What is **==Node.js==**?

- An open source server enviroment
- Runs on various platforms (Windows, Linux, Unix, Mac OS…)
- Uses JavaScript on the server

---

## Download ==Node.js==

> [!info] Node.js  
> Node.  
> [https://nodejs.org](https://nodejs.org)  

---

## Example:

https://github.com/liemgumball/nodejs-practice

## Target:

- ==Understand the== ==**Node.js**== ==asynchronous programming model==
- Understand the asynchronous & control flow in Node.js
- ==Create simple== ==**Node.js**== ==applications using modules & web framework==
- ==Develop a simple web application using framework like Express==
- Discover tips for testing your web application
- Debug and diagnose issues in your Node.js applications
- Build and deploy scalable microservices architecture with the power of Node.js

## Getting Started

Example:

```JavaScript
var http = require('http')

http.createServer(function (req, res) {
	res.writeHead(200, {'Content-Type': 'text/html'})
	res.end('Hello world!')
}).listen(8080)
```

Run:

```Bash
node first.js
```

---

## Handling I/O (input/ output)

> [!important] The core APIs provided by
> 
> ==**Node.js**== that allow us to interact with the standard I/O, the file system, and the network stack.

- `stdin` (standard in) refers to an input stream that a program can use to read input
- `stdout` (standard out) refers to the stream that is used to write the output
- `stderr` (standard error) is a separate stream to `stdout` that is typically reserved for outputting errors and diagnostic data.

```JavaScript
process.stdin.on('data', (data) => {
	const name = data.toString().trim().toUpperCase()
	if (name !== '') {
		process.stdout.write(`Hello ${name}!`)
	} else {
		process.stderr.write('Input was empty.')
	}
})
```

`process.stdin`, `process.stdout`, and `process.stderr` are all properties on the process object. A global `process` object provides the information and control of the ==**Node.js**== process.

## Node Modules

==Modules== are considered same as ==**JavaScript**== libraries

> [!info] Index | Node.js v21.6.2 Documentation  
>  
> [https://nodejs.org/api/](https://nodejs.org/api/)  

### Built-in Modules

|Module|Description|
|---|---|
|`[assert](https://www.w3schools.com/nodejs/ref_assert.asp)`|Provides a set of assertion tests|
|`[buffer](https://www.w3schools.com/nodejs/ref_buffer.asp)`|To handle binary data|
|`child_process`|To run a child process|
|`[cluster](https://www.w3schools.com/nodejs/ref_cluster.asp)`|To split a single Node process into multiple processes|
|`[crypto](https://www.w3schools.com/nodejs/ref_crypto.asp)`|To handle OpenSSL cryptographic functions|
|`[dgram](https://www.w3schools.com/nodejs/ref_dgram.asp)`|Provides implementation of UDP datagram sockets|
|`[dns](https://www.w3schools.com/nodejs/ref_dns.asp)`|To do DNS lookups and name resolution functions|
|`domain`|Deprecated. To handle unhandled errors|
|`[events](https://www.w3schools.com/nodejs/ref_events.asp)`|To handle events|
|`[fs](https://www.w3schools.com/nodejs/ref_fs.asp)`|To handle the file system|
|`[http](https://www.w3schools.com/nodejs/ref_http.asp)`|To make Node.js act as an HTTP server|
|`[https](https://www.w3schools.com/nodejs/ref_https.asp)`|To make Node.js act as an HTTPS server.|
|`[net](https://www.w3schools.com/nodejs/ref_net.asp)`|To create servers and clients|
|`[os](https://www.w3schools.com/nodejs/ref_os.asp)`|Provides information about the operation system|
|`[path](https://www.w3schools.com/nodejs/ref_path.asp)`|To handle file paths|
|`punycode`|Deprecated. A character encoding scheme|
|`[querystring](https://www.w3schools.com/nodejs/ref_querystring.asp)`|To handle URL query strings|
|`[readline](https://www.w3schools.com/nodejs/ref_readline.asp)`|To handle readable streams one line at the time|
|`[stream](https://www.w3schools.com/nodejs/ref_stream.asp)`|To handle streaming data|
|`[string_decoder](https://www.w3schools.com/nodejs/ref_string_decoder.asp)`|To decode buffer objects into strings|
|`[timers](https://www.w3schools.com/nodejs/ref_timers.asp)`|To execute a function after a given number of milliseconds|
|`[tls](https://www.w3schools.com/nodejs/ref_tls.asp)`|To implement TLS and SSL protocols|
|`tty`|Provides classes used by a text terminal|
|`[url](https://www.w3schools.com/nodejs/ref_url.asp)`|To parse URL strings|
|`[util](https://www.w3schools.com/nodejs/ref_util.asp)`|To access utility functions|
|`v8`|To access information about V8 (the JavaScript engine)|
|`[vm](https://www.w3schools.com/nodejs/ref_vm.asp)`|To compile JavaScript code in a virtual machine|
|`[zlib](https://www.w3schools.com/nodejs/ref_zlib.asp)`|To compress or decompress files|

### File System Module

Allow us to work with file on computer

Example:

```JavaScript
const fs = require('fs')
const path = require('path')

const filepath = path.join(process.cwd(), 'hello.txt')

fs.readFile(filepath, 'utf8', (err, data) => {
	if (!err) {
		console.log('Contents: ', data)
		fs.writeFileSync(filepath, data.toUpperCase())
		console.log('Updated!')
	} else throw err
})
```

This module allow us to:

- Create Files
- Update Files
- Delete Files
- Rename Files
- [Upload Files](https://www.w3schools.com/nodejs/nodejs_uploadfiles.asp)

### Inspecting file metadata

The `fs` module generally provides APIs that are modeled around **Portable Operating System Interface (POSIX)** functions. The `fs` module includes APIs that facilitate the  
reading of directories and file ==metadata==.

### Checking file access

It is recommended that if you're attempting to ==read==, ==write==, or ==edit== a file, you follow the approach of handling the error if the file is not found.

- `fs.access()`
- `fs.accessSync()`

```JavaScript
import { access, constants } from 'node:fs';

const file = 'package.json';

// Check if the file exists in the current directory.
access(file, constants.F_OK, (err) => {
  console.log(`${file} ${err ? 'does not exist' : 'exists'}`);
});

// Check if the file is readable.
access(file, constants.R_OK, (err) => {
  console.log(`${file} ${err ? 'is not readable' : 'is readable'}`);
});

// Check if the file is writable.
access(file, constants.W_OK, (err) => {
  console.log(`${file} ${err ? 'is not writable' : 'is writable'}`);
});

// Check if the file is readable and writable.
access(file, constants.R_OK | constants.W_OK, (err) => {
  console.log(`${file} ${err ? 'is not' : 'is'} readable and writable`);
});
```

### Modifying file permissions

The ==**Node.js**== `fs` module provides APIs that can be used to alter the permissions on a given file.

- `fs.chmod()`
- `fs.chmodSync()`

```JavaScript
import { chmod } from 'node:fs';

chmod('my_file.txt', 0o775, (err) => {
  if (err) throw err;
  console.log('The permissions for file "my_file.txt" have been changed!');
});
```

File modes:

|**Constant**|**Octal**|**Description**|
|---|---|---|
|`fs.constants.S_IRUSR`|`0o400`|read by owner|
|`fs.constants.S_IWUSR`|`0o200`|write by owner|
|`fs.constants.S_IXUSR`|`0o100`|execute/search by owner|
|`fs.constants.S_IRGRP`|`0o40`|read by group|
|`fs.constants.S_IWGRP`|`0o20`|write by group|
|`fs.constants.S_IXGRP`|`0o10`|execute/search by group|
|`fs.constants.S_IROTH`|`0o4`|read by others|
|`fs.constants.S_IWOTH`|`0o2`|write by others|
|`fs.constants.S_IXOTH`|`0o1`|execute/search by others|

An easier method of constructing the `mode` is to use a sequence of three octal digits (e.g. `765`). The left-most digit (`7` in the example), specifies the permissions for the file owner. The middle digit (`6` in the example), specifies permissions for the group. The right-most digit (`5` in the example), specifies the permissions for others.

|**Number**|**Description**|
|---|---|
|`7`|read, write, and execute|
|`6`|read and write|
|`5`|read and execute|
|`4`|read only|
|`3`|write and execute|
|`2`|write only|
|`1`|execute only|
|`0`|no permission|

For example, the octal value `0o765` means:

- The owner may read, write, and execute the file.
- The group may read and write the file.
- Others may read and execute the file.

### Modifying file owner

- `fs.chown()`
- `fs.chownSync()`

### Inspecting symbolic links

A symbolic ==link==, or ==symlink==, is a special file that stores a reference to another file or directory. When the stat or `statSync()` function from the Inspecting file metadata recipe is run on a symbolic link, it will return information about the file the symbolic link references, rather than the symbolic link itself.

1. Created a symbolic link
    
    ```Shell
    ln -s file.txt link-to-file
    ```
    
2. Now, you can use the ==**Node.js**== **REPL (Read-Eval-Print Loop)** to test the `lstatSync()` function. The ==**Node.js**== **REPL** is an interactive ==shell== we can pass statements to, and it will evaluate them and return the result to the user.
3. To enter the **Node.js REPL**
    
    ```Shell
    $ node
    
    Welcome to Node.js v14.0.0.
    Type ".help" for more information.
    >
    ```
    
4. Test the `lstatSync()`
    
    ```Shell
    > console.log("Hello World!");
    Hello World!
    > fs.lstatSync("link-to-file");
    Stats {
    	dev: 16777224,
    	...
    }
    ```
    

### Watching for file updates

`fs` module provides functionality that enables you to watch files and track when files or directories are ==created==, ==updated==, or ==deleted==.

```JavaScript
const fs = require('fs')
const file = './file.txt'

fs.watchFile(file, (curr, pre) => {
	return console.log(`${file} updated ${curr.mtime}`)
})
```

Reference:

> [!info] File system | Node.js v21.6.2 Documentation  
> The node:fs module enables interacting with the file system in a  
> [https://nodejs.org/api/fs.html](https://nodejs.org/api/fs.html)  

### Creating TCP server and client communication

==**Sockets**== allow machines and devices to communicate. ==**Sockets**== are also used to coordinate I/O across networks. The term _socket_ is used to refer to ==one endpoint of a two-way network== communication link. ==**Sockets**== enable us to build _real-time_ web applications, such as instant messaging applications.

> [!important] ==**TCP**==
> 
> stands for _**Transmission Control Protocol**_. ==**TCP**== provides a standard that allows devices to communicate over a network.

```JavaScript
const net = require('net')

const HOSTNAME = 'localhost'
const PORT = 3000

net.createServer((socket) => {
	console.log('Client connected!')

	socket.on('data', (name) => {
		socket.write(`Hello ${name}!`)
	})
}).listen(PORT, HOSTNAME)
```

```JavaScript
const net = require('net')

const HOSTNAME = 'localhost'
const PORT = 3000

const socket = net.connect(PORT, HOSTNAME)

process.stdin.on('data', (data) => {
	socket.write(data.toString().replace(/\n/g, ''))
})

socket.on('data', (data) => {
	console.log(`${data}`)
})
```

The recipe used the `createServer()` function from the `http` module and the `net` function to create the server

> [!info] Net | Node.js v21.6.2 Documentation  
> The node:net module provides an asynchronous network API for creating stream-based  
> [https://nodejs.org/api/net.html](https://nodejs.org/api/net.html)  

For some communications, ==**UDP**== is more appropriate than ==**TCP**==. Let's take a look at what  
==**UDP**== sockets are, what they're used for, and how to implement a ==**UDP**== socket.

> [!important] ==**UDP**==
> 
> stands for _**User Datagram Protocol.**_ ==**UDP**== is a ==connectionless== protocol. Unlike ==**TCP**==, the protocol ==does not== establish a connection before sending data. ==**UDP**== is typically used for _video calling_, _gaming_, or _streaming_—because in these cases, ==minimizing delay== is important.

```JavaScript
const dgram = require('dgram')

const socket = dgram.createSocket('udp6')
socket.bind(PORT)
```

### URL Module

This module splits up a web address into readable parts.

|Method|Description|
|---|---|
|`url.format()`|Returns a formatted URL string|
|`url.parse()`|Returns a URL object|
|`url.resolve()`|Resolves a URL|

> [!info] URL | Node.js v21.6.2 Documentation  
> The node:url module provides utilities for URL resolution and parsing.  
> [https://nodejs.org/api/url.html](https://nodejs.org/api/url.html)  

---

## Using web protocol

[[Web protocol with Node.js]]

## Developing ==Node.js== module

[[Developing modules]]

## Exploring ==Node.js== web framework

[[Express framework]]

## Working with Database

Many applications require `data` _access_ and _storage_, and in many cases, a traditional ==relational database== suits the application's requirements. In a ==relational database==, the data will likely have a defined _relationship_, _organized_ into ==tables==.

However, more recently there has been the emergence of ==_non-relational databases_==, often falling under the term ==**NoSQL**== databases. ==**NoSQL**== databases suit data where there isn't an ==easily predefined structure==, or where ==flexibility== in the data structure is required.

[[Working with SQL databases]]

[[Working with NoSQL databases]]

## Persisting data

[[Persisting data with Redis]]

---

## Testing with ==Node.js==

==Testing== enables to identify ==bugs== in the code more quickly and efficiently. Test cases should be written to verify that each piece of code is yielding the ==expected output== or results.

[[Testing with Jest]]

---

## Securing ==Node.js== applications

[[Node.js securing]]

---

## ==Node.js== microservices

> [!important] The term
> 
> _microservices_ is used to describe applications that have been built on the basis of the ==microservice architecture paradigm==.

This architecture encourages larger applications to be built as a set of smaller ==modular applications==, where each application focuses on one key concern. Ensuring that an application ==only serves one purpose== means that the application can be ==optimized to best== serve that purpose.

[[Deploying Node.js microservices]]

---

## Debugging Node.js

> [!important] The ==asynchronous== nature of ==**JavaScript**== and ==**Node.js**== makes the debugging process non-trivial. However, over the past decade, ==**Node.js**== has matured as a technology, and the ==debugging capabilities== and ==facilities== have improved accordingly.

### Diagnosing issues with ==**Browser DevTools**==

1. ==**Node.js**== exposes a debugging utility via the `--inspect` process flag, which enables us to debug and profile our ==**Node.js**== processes using the ==**Browser DevTools**== interface.
    
    ```Bash
    node --inspect server.js
    ```
    
    ![[Class Notes/NodeJS/attachments/Untitled.png|Untitled.png]]
    
2. Observe that our `server.js` is showing up as a **Remote Target**
    
    ![[Class Notes/NodeJS/attachments/Untitled 1.png|Untitled 1.png]]
    
3. From here we can add some `breakpoints` on the code for debugging. The app will paused on the `breakpoints`

> [!important] **Pausing a process on start**
> 
>   
> ==**Node.js**== also provides a flag `--inspect-brk` that we can use to pause an application on start. This feature enables us to set up breakpoints before anything executes

---

### Logging with Node.js

Effective logging can help you understand what is going on in an application.

`express-pino-logger` is a ==middleware== that enables ==**Pino**== ==logging== on our **Express.js** web server. We import these independently so that we can interact with the ==pino logger== both directly and via our ==middleware==

```JavaScript
const express = require('express')
const app = express()
const PORT = 3000

const pino = require('pino')()
const logger = require('express-pino-logger')({
	instance: pino,
})

app.use(logger)

app.get('/', (req, res) => {
	const randomNumber = getRandomNumber()
	req.log.info('Generating random number')
	res.send(`${randomNumber}`)
})

app.listen(PORT, () =>
	pino.info(`Server listening on
port ${PORT}`)
)
```

---

### Enabling debug logs

`debug` is a popular library, used by many notable frameworks, including the **Express.js** and ==**Koa.js**== web frameworks and the ==**Mocha**== test framework. `debug` is a ==small== ==**JavaScript**== ==debugging utility based== on the debugging technique used in ==**Node.js**== core.

To turn on `debug` logging, start your server with the following command

```Bash
DEBUG=* node server.js
```

  

We can also filter which debug logs are output. Let just see the **Express.js** ==router actions==.

```Bash
DEBUG=express:router* node server.js
```

---

### Enabling ==Node.js core== debug logs

When debugging some problems in your applications, it can be useful to have insight into the ==internals== of ==**Node.js**== and how it handles the execution of your program. ==**Node.js**== provides ==debug logs== that we can enable to help us understand what is happening ==internally== in ==**Node.js**==

Set the `NODE_DEBUG` variable to the internal flag we wish to log

The ==internal flags== align with specific ==subsystems== of ==**Node.js**==, such as `timer` or `http`

```Bash
NODE_DEBUG=<subsystem> node server.js

# example 
NODE_DEBUG=http,timer node server.js
```

---

### Increasing stack trace size

A stack trace, sometimes referred to as a ==stack backtrace==, is defined as a ==list of stack frames==. When your ==**Node.js**== process hits an `error`, a stack trace is shown ==detailing the function== that experienced the `error`, and the ==functions== that it was ==called by==.

Use the `--stack-trace-limit` process flag

```Bash
node --stack-trace-limit=20 server.js
```

---

### Creating diagnostic reports

The ==diagnostic report utility== has been available behind a process flag since ==**Node.js v11.8.0.**== The ==diagnostic report utility== allows you to generate a ==report containing diagnostic data== on demand or when certain events occur.

```JavaScript
const http = require("http");
const path = require("path");

process.report.directory = path.join(__dirname,"reports");
process.report.filename = "my-diagnostic-report.json"; 

http.get("hello://localhost:3000", (response) => {});
```

  

If we run the application, we should expect to see the following uncaught `ERR_INVALID_PROTOCOL` error

```Bash
$ node server.js
_http_client.js:155
		throw new ERR_INVALID_PROTOCOL(protocol,
expectedProtocol);
		^
		TypeError [ERR_INVALID_PROTOCOL]: Protocol "hello:" not
supported. Expected "http:"
		at new ClientRequest (_http_client.js:155:11)
		at request (http.js:47:10)
		at Object.get (http.js:51:15)
		at Object.<anonymous> (/Users/bethgriggs/Node-
Cookbook/Chapter13/diagnostic-report/server.js:7:6)
		at Module._compile (internal/modules/cjs/loader.
js:1200:30)
		at Object.Module._extensions..js (internal/modules/
cjs/loader.js:1220:10)
		at Module.load (internal/modules/cjs/loader.
js:1049:32)
		at Function.Module._load (internal/modules/cjs/
loader.js:937:14)
		at Function.executeUserEntryPoint [as runMain]
(internal/modules/run_main.js:71:12)
		at internal/main/run_main_module.js:17:47 {
code: 'ERR_INVALID_PROTOCOL'
}
```

  

To enable the diagnostic report feature, process with the `--report-uncaught-exception` flag

```Bash
node --report-uncaught-exception server.js
```

  

It should have been created in the reports directory with the name `my-diagnostic-report.json`

  

---

## OPEN QUESTIONS

### What is the difference between JavaScript and Node.js?

|**JavaScript**|**Node.js**|
|---|---|
|==A Programming language== primarily used for front-end web development|==A runtime environment== for executing **JavaScript** code outside of a web browser|
|It runs in web browsers and is used to make web pages interactive|It allows JavaScript to be used for server-side programming|
|**JavaScript** can ==manipulate== the **HTML** and **CSS** of a webpage|**Node.js** uses an ==event-driven==, ==non-blocking I/O== model that makes it lightweight and efficient, suitable for building scalable ==network applications==|
||It comes with a set of ==built-in modules== that provide functionalities for ==file system I/O==, ==networking== (HTTP, TCP, UDP, etc.), and more|
||**Node.js** is commonly used for building ==web servers==, ==APIs==, real-time chat applications, streaming applications, and various other types of backend systems|

### What do you mean by Asynchronous API?

It is an interface provided by software components that allows operations to be performed asynchronously.

> [!important] It’s the main difference between
> 
> **Node.js** and some other web-server

Asynchronous APIs are particularly useful in scenarios where certain operations may take a significant amount of time to complete, such as network requests, file I/O operations, or database queries

### Example

How **PHP** and **ASP** handles file requests

1. Sends the task to the computer's file system.
2. Waits while the file system opens and reads the file.
3. Returns the content to the client.
4. Ready to handle the next request.

---

How **Node.js** handles file requests

1. Sends the task to the computer's file system.
2. Ready to handle the next request (thanks to **==Asynchronous API==**)
3. When the file system has opened and read the file, the server returns the content to the client.

### What are the benefits of using Node.js?

1. Asynchronous and event-driven architecture
2. Single language for both ==client-side== and ==server-side== development (**JavaScript**)
3. Rich ==ecosystem of libraries== and frameworks via `npm`
4. Fast execution speed due to the ==V8== ==**JavaScript**== ==engine==
5. Scalability for handling large volumes of traffic
6. Active ==community== support and resources
7. Cross-platform compatibility
8. Lightweight and efficient for building highly scalable applications.

### What is REPL in the context of Node?

**REPL** stands for **Read-Eval-Print Loop**. In the context of **Node.js**, **REPL** refers to an interactive programming environment that allows you to enter **JavaScript** ==commands== and immediately see their results

It provides a way to experiment with **JavaScript** code, ==test small code== snippets, and ==quickly evaluate expressions== without needing to create a full-fledged script or application.

### What is npm? What is package.json?

`**npm**` **(Node Package Manager)**: the default package manager for **Node.js**, used to ==install==, ==manage==, and ==share== packages of **JavaScript** code. It allows developers to easily add ==dependencies== to their projects, manage versions, and handle project dependencies efficiently.

`**package.json**`: a metadata file used in **Node.js** projects to define various properties and settings for the project, including its ==name==, ==version==, ==description==, ==dependencies==, ==scripts==, and more. It serves as the central configuration file for **Node.js** projects and is used by `npm` to manage project dependencies and scripts.

### What is Callback?

A `callback` is a ==function== that is passed ==as an argument== to ==another function== and is executed at a later time or under certain conditions. In **JavaScript**, callbacks are commonly used in ==asynchronous programming== to handle tasks that depend on the completion of other tasks or operations

### What are the two types of API functions in Node.js?

1. **Synchronous API functions**: These functions ==block the execution== of the program until the operation is completed. They are straightforward to use ==but can lead to== ==performance issues==, especially in applications ==handling multiple concurrent requests==, as they halt the program until the operation finishes.
2. **Asynchronous API functions**: These functions initiate an operation and then continue executing the program without waiting for the operation to complete.

### What is a blocking code? How does Node prevent blocking code?

- ==**Blocking code**== refers to code that halts the execution of a program until a particular operation is completed. In a blocking code scenario, if one operation takes a significant amount of time to finish (e.g., reading data from a file or making a network request), the entire program will be ==delayed== until that operation completes
- **Node.js** prevents blocking code by utilizing an ==asynchronous==, ==non-blocking I/O model==, ==event loop==, and ==callback functions==, enabling efficient handling of multiple concurrent operations without halting the entire program.
    
    Here's an example how it works:
    

### What is Libuv?

`Libuv` is a multi-platform ==**C**== library that provides ==asynchronous I/O support== _(file system operations, network requests, timers …)_, ==event loop==, ==cross-platform supports==, ==thread pools== and other fundamental features for building networking applications. It serves as the ==core foundation== for ==handling asynchronous operations== in **Node.js**

### What is Event Loop?

It is a ==continuous process== in **asynchronous programming** that ==waits for== and ==dispatches== events or messages in a program, ensuring non-blocking I/O operations and asynchronous execution of tasks.

It manages events from a ==queue==, executes their associated ==callback functions==, and repeats the process indefinitely, enabling responsive and efficient ==handling of multiple concurrent tasks==.

[![](https://miro.medium.com/v2/resize:fit:1400/1*7coLKNPemPd9o40PmUvuvQ.gif)](https://miro.medium.com/v2/resize:fit:1400/1*7coLKNPemPd9o40PmUvuvQ.gif)

### What is an Event Emitter in Node.js?

==**Event Emitter**== is a `built-in class` that allows objects to emit and handle custom events. It provides a way to implement the ==observer== pattern, enabling communication between different parts of a **Node.js** application.

**==Event Emitters==** are used extensively in ==**Node.js**== for building ==event-driven architectures==, such as handling ==HTTP requests==, ==file system operations==, ==network communication==, and more. They provide a flexible and efficient way to implement ==event-driven programming paradigms==, allowing for modular, scalable, and maintainable code.

### What is the Async/Await function in Node.js?

The `**async/await**` functions in **Node.js** are a modern way of writing ==asynchronous code== that looks and behaves ==more like synchronous code==. It provides a syntactic sugar on top of promises, ==making asynchronous code easier to read and write==

`**async/await**` simplifies asynchronous code by making it appear synchronous, which can improve readability and maintainability, especially for complex asynchronous operations.

### When should we use Promise instead of Async/Await?

Both promises and `async/await` are tools for handling asynchronous code in **JavaScript**, and each has its advantages depending on the specific use case

Use Promises when:

- **Compatibility**: When working with codebases that ==do not support async/await==, or if you need to integrate with libraries or APIs that return promises, using promises directly is necessary.
- **Sequential Operations**: If you need to perform a sequence of asynchronous operations where each operation depends on the result of the previous one, promises with chaining (`**then**`) can provide a clear and concise way to express this sequence.
- **Error Handling**: Promises allow you to use `**.catch()**` at the end of a chain to catch errors that occur at any point in the chain, making it easier to handle errors globally or at specific points in the code.