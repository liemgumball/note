
> **[NodeJS](NodeJS.md)**  can be used as a tool to build a variety of systems, including *microservices*, real-time applications such as *chatbots*, and even *robotics*
> 

[Express - Node.js web application framework](http://expressjs.com)

## Target

- Building web applications with **Express.js**

---

## Building web applications with *Express.js*

<aside>
💡 The **Express.js** framework abstracts the underlying **Node.js** core web protocol APIs provided by the `http` and `https` core modules. **Express.js** provides an interface for *routing* and *adding middleware*.

</aside>

[Express 4.x - API Reference](https://expressjs.com/en/4x/api.html)

### Getting started

```jsx
const express = require('express')

const router = express.Router()

router.get('/', (req, res) => {
	const title = 'Express'
	res.send(`
    <html>
      <head>
        <title> ${title} </title>
        <link rel="stylesheet" href="styles.css">
      </head>
      <body>
        <h1> ${title} </h1>
        <p> Welcome to ${title} </p>
      </body>
    </html>
  `)
})

module.exports = router
```

```jsx
const express = require('express')
const path = require('path')
const index = require('./routes')

const PORT = process.env.PORT || 3000

const app = express()

app.use(express.static(path.join(__dirname, 'public')))
app.use('/', index)

app.listen(PORT, () => {
	console.log(`Server listening on port ${PORT}`)
})
```

The `app.use()` function is used to register middleware. In the context of **Express.js**, middleware means functions that execute during the life cycle of a request. **Express.js** middleware functions have access to the request `(req)` and response `(res)` objects. Middleware can *execute code*, *alter* or *operate* on the request and response objects, `end` the request-response cycle, or *call another middleware*. The last middleware must end the request-response cycle, otherwise the request will hang.

---

Let's explore more of the core functionality provided by **Express**, including *adding* views and *creating* custom middleware

### Adding views with Express.js & EJS

**Express.js** is often used to generate and serve **HTML** web pages.

We can configure **Express.js** to use the **EJS** view engine, created an **EJS** template, and instructed **Express.js** to render the template on the `index` (/) route.

```html
<html>
	<head>
		<title><%= title %></title>
		<link rel="stylesheet" href="styles.css" />
	</head>
	<body>
		<h1><%= title %></h1>
		<p>Welcome to <%= title %></p>
	</body>
</html>
```

```jsx
const express = require('express')

const router = express.Router()

router.get('/', (req, res) => {
	const title = 'Express'
	res.render('index', { title: 'Express with EJS' })
})

module.exports = router
```

```jsx
const express = require('express')
const path = require('path')

const PORT = process.env.PORT || 3000

const app = express()

app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'ejs')

app.use(express.static(path.join(__dirname, 'public')))
app.use('/', require('./routes'))

app.listen(PORT, () => {
	console.log(`Server listening on port ${PORT}`)
})
```

### Custom middleware

```jsx
module.exports = logger = () => (req, res, next) => {
	console.log(
		"Request received in middleware's logger: ",
		req.method,
		req.url
	)
	next()
}
```

```jsx
const app = express()
// ...
app.use(require('./middlewares/logger')())
app.use(express.static(path.join(__dirname, 'public')))
app.use('/', require('./routes'))
// ...
```

---

## Generating an Express.js application

**Express.js** provides a generator that scaffolds you a skeleton application. You can run the generator from *Terminal* using `npx`

[Express application generator](https://expressjs.com/en/starter/generator.html)

```bash
npx express-generator --view=ejs express-generated-app
```

<aside>
📌 **Jade versus Pug**
**Jade** is the former name for the **Pug** templating engine. The express-generator will currently default to using **Jade** if you omit the `--view` argument, but the **Jade** module has not been maintained since the rename to **Pug**. It is therefore always recommended to specify the `--view` or `--no-view` arguments, as the jade module has been deprecated.

</aside>

We can also specify which **CSS** engine you'd like to use via the `--css` argument.

- LESS
- Stylus
- Compass
- Sass

### Handling POST requests and route parameters

```jsx
const express = require('express')

const router = express.Router()

router.get('/:name?', function (req, res) {
	const title = 'Express'
	const name = req.params.name
	res.send(`
	  <html>
		  <head>
			  <title> ${title} </title>
			  <link rel="stylesheet" href="styles.css">
		  </head>
		  <body>
			  <h1> ${title} </h1>
			  <p> Welcome to ${title}${name ? `, ${name}.` : ''} </p>
			  <form method=POST action=data>
				  Name: <input name=name><input type=submit>
			  </form>
		  </body>
	  </html>
  `)
})

router.post('/data', function (req, res) {
	res.redirect(`/${req.body.name}`)
})

module.exports = router

```

```jsx
const app = express()

app.use(require('body-parser').urlencoded({ extended: false }))
app.use(express.static(path.join(__dirname, 'public')))
app.use('/', require('./routes'))
//...
```

<aside>
📌 **Important Note**
The `{ extended: false }` option instructs body-parser to use the `querystring` library for URL parsing. Omitting this setting or setting it to true will instruct body-parser to use the `qs` library instead. The main difference is that `qs` supports nested objects. However, `qs` has options that if not configured correctly could lead to denial-of-service attacks.

</aside>

### Router methods

*Routing* determines how an application responds to a request at a given *endpoint*. Typically, an endpoint is expressed by a **URL** (path) and the **HTTP** request method. **Express's** `Router` ****object exposes methods that we can use to create endpoints in our application.

### `NODE_ENV` environment variable

**Express.js** anticipates `NODE_ENV` as a variable name. `NODE_ENV` is used to specify which environment the application is running in.

```jsx
const dev = process.env.NODE_ENV !== "production";
if (dev) {
// dev specific behaviors here
}
```

```bash
$ NODE_ENV=production node index.js
```