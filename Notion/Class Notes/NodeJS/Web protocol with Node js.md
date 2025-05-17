
> ***Node.js** was built with web servers in mind.*
> 

---

Using [NodeJS](NodeJS.md), we can quickly create a web server with a few lines of code, allowing us to customize the behavior of our server.

## Target

- Using `http` module to make **HTTP** requests
- Building an **HTTP** server to accept **GET** requests
- Handling **HTTP** **POST** requests
- Using formidable to handle file uploads
- Using `ws` to create a **WebSocket** server
- Sending an automated email using your own **SMTP** server

<aside>
💡 **HTTP** (***HyperText Transfer Protocol***) is a stateless protocol that was originally designed to facilitate communication between web browsers and servers.

</aside>

## Making request

```jsx
const http = require('http')

http.get('http://example.com', (res) => res.pipe(process.stdout))
```

```jsx
const payload = `{"name":"liem","job":"dev"}`
const opts = {
	hostname: 'www.httpbin.org',
	path: '/post',
	method: 'POST',
	headers: {
		'Content-Type': 'application/json',
		'Content-Length': Buffer.byteLength(payload),
	},
}

// send the POST request
const req = http.request(opts, (res) => {
	process.stdout.write('Status Code: ' + res.statusCode + '\n')
	process.stdout.write('Body: ')
	res.pipe(process.stdout)
})

// catch any errors that occur on the request
req.on('error', (err) => console.error('Error: ', err))

// finally send the request payload
req.end(payload)
```

---

## Building an HTTP server

```jsx
var http = require('http');
var url = require('url');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  var q = url.parse(req.url, true).query;
  var txt = q.year + " " + q.month;
  res.end(txt);
}).listen(8080,'localhost');
```

The **Node.js** core `http` module is built on top of, and interacts with, the **Node.js** core `net` module. The net module interacts with an underlying **C** library built into **Node.js,** called `libuv`. The `libuv` **C** library handles network ***socket input/output (I/O)*** and also handles the passing of data between the **C** and **JavaScript** layers.

---

## Using `formiable` module to upload files

> *A **Node.js** module for parsing form data, especially file uploads.*
> 

[npm: formidable](https://www.npmjs.com/package/formidable)

Uploading a file to the web is a common activity, be it an *image*, a *video*, or a *document*. Files require different handling compared to simple **POST** data. Browsers embed files being uploaded into *multipart messages*.
Multipart messages allow multiple pieces of content to be combined into one payload. To handle multipart messages, we need to use a multipart parser.

```jsx
const fs = require('fs')
const path = require('path')
const http = require('http')
const { formidable } = require('formidable') //

const form = fs.readFileSync(path.join(__dirname, 'public', 'form.html'),'utf8')

http.createServer((req, res) => {
	if (req.method === 'GET') {
		get(res)
		return
	}
	if (req.method === 'POST') {
		post(req, res)
		return
	}
	return error(405, res)
}).listen(3000)

// get the form.html
const get = (res) => {
	res.writeHead(200, {
		'Content-Type': 'text/html',
	})
	res.end(form)
}

// POST method with encrypt: `multipart/form-data` 
const post = (req, res) => {
	if (!/multipart\/form-data/.test(req.headers['content-type']))
		return error(415, res)
	else {
		const form = formidable({
			multiples: true,
			uploadDir: './uploads',
		})

		form.parse(req, (err, fields, files) => {
			if (err) return err
			res.writeHead(200, {
				'Content-Type': 'application/json',
			})
			res.end(JSON.stringify({ fields, files }))
		})
	}
}

// handling error response
const error = (code, res) => {
	res.statusCode = code
	res.end('error ' + code + ' : ' + http.STATUS_CODES[code])
}
```

<aside>
📌 Allowing the upload of any file type of any size makes your server vulnerable to *Denial-of-Service* (**DoS**) attacks. Attackers could purposely try to upload excessively large or malicious files to slow down your server. It is recommended that you add both client-side and server-side validation to restrict the file *types* and *sizes* that your server will accept.

</aside>

---

## Using `ws` to create a WebSocket server

<aside>
💡 The **WebSocket** protocol enables two-way communication between a browser and a server. **WebSockets** are commonly leveraged for building real-time web applications, such as instant messaging clients.

</aside>

[npm: ws](https://www.npmjs.com/package/ws)

```jsx
const WebSocket = require('ws')

const WebSocketServer = new WebSocket.Server({
	host: 'localhost',
	port: 3000,
})

WebSocketServer.on('connection', (socket, req) => {
	socket.on('message', (message) => {
		console.log('received: %s', message)
		if (message.toString() === 'hello') socket.send('world')
	})
})
```

```jsx
const WebSocket = require('ws')
const ws = new WebSocket('ws://localhost:3000')

ws.on('open', () => {
	console.log('Connected')
})

ws.on('close', () => {
	console.log('Disconnected')
})

ws.on('error', (err) => {
	console.error(err)
})

ws.on('message', (msg) => {
	console.log('Received: ' + msg)
})

setInterval(() => {
	ws.send('hello')
}, 3000)
```

---

## Sending an automated email using your own SMTP server

<aside>
💡 **SMTP** stands for *Simple Mail Transfer Protocol* and is a protocol for sending emails.

</aside>

```jsx
const { SMTPServer } = require('smtp-server')

const PORT = 4321

const server = new SMTPServer({
	disabledCommands: ['STARTTLS', 'AUTH'],
	logger: true,
})

server.on('error', (err) => console.error)

server.listen(PORT)
```

Added the `disabledCommands: ['STARTTLS', 'AUTH']` option. This option `disabled` *Transport Layer Security* **(TLS)** support and authentication for simplicity. However, in production, it would not be recommended to disable **TLS** support and authentication. Instead, it would be recommended to enforce **TLS**. We can do this with the `smtp-server` module by specifying the `secure:true` option.

---

To send an email with **Node.js**, we can use the `nodemailer` module. This module is provided by the same organization as the `smtp-server` module used in the S*ending an automated email using our own **SMTP*** server recipe.

```jsx
const nm = require('nodemailer')

const transporter = nm.createTransport({
	host: 'localhost',
	port: 4321,
})

transporter.sendMail(
	{
		from: 'beth@example.com',
		to: 'laddie@example.com',
		subject: 'Hello',
		text: 'Hello world!',
	},
	(err, info) => {
		if (err) console.error(err)
		else console.log('Message sent: ', info)
	}
)
```

- Multiple receivers
    
    ```jsx
    var mailOptions = {
      from: 'youremail@gmail.com',
      to: 'myfriend@yahoo.com, myotherfriend@yahoo.com',
      subject: 'Sending Email using Node.js',
      text: 'That was easy!'
    }
    ```
    
- Send HTML
    
    ```jsx
    var mailOptions = {
      from: 'youremail@gmail.com',
      to: 'myfriend@yahoo.com',
      subject: 'Sending Email using Node.js',
      html: '<h1>Welcome</h1><p>That was easy!</p>'
    }
    ```