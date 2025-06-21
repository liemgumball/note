> [!important] Always take certain precautions to ensure the application built in secure

### Target

- Detecting known dependency vulnerabilities
- ==Authentication with== **Express.js**
- Setting HTTP headers with `helmet`
- Protecting against HTTP parameter pollution attacks
- Preventing JSON pollution
- Preventing cross-site scripting attacks
- Guarding against cross-site request forgery attacks

## Detecting known dependency vulnerabilities

1. For example we install an outdated package from `npm`
    
    ```Bash
    npm install express@4.15.0
    ```
    
2. We get warning that this **Express** version is not recommended for production
    
    ![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled.png|Untitled.png]]
    
3. Run the below command to see details
    
    ```Bash
    npm audit
    ```
    
    ![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled 1.png|Untitled 1.png]]
    
4. Run to fix the vulnerabilities
    
    ```Bash
    npm audit fix
    ```
    
    ![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled 2.png|Untitled 2.png]]
    

---

## Authentication with Express.js

Many web applications require a ==login system==. Often, users of a website have different ==privileges==, and to ==ascertain== which resources they're able to access, they must first be identified via ==_authentication_==

Building a login system using the `express-session` module to handle sessions

```JavaScript
const express = require('express')
const bodyParser = require('body-parser')
const { join } = require('path')
const session = require('express-session')

const index = require('./routes/index')
const auth = require('./routes/auth')

const app = express()

app.use(
	session({
		name: 'SESSIONID',
		secret: 'Node Cookbook',
		resave: false,
		saveUninitialized: false,
	})
)
app.set('views', join(__dirname, 'views'))
app.set('view engine', 'ejs')

app.use(bodyParser.urlencoded({ extended: false }))

app.use('/', index)
app.use('/auth', auth)

app.listen(3000, () => {
	console.log('Server listening on port 3000')
})
```

```JavaScript
const { Router } = require('express')
const router = Router()

router.get('/login', (req, res) => {
	res.render('login', { fail: false })
})

router.post('/login', (req, res, next) => {
	if (req.session.user) {
		res.redirect('/')
		next()
		return
	}
	if (req.body.username === 'liem' && req.body.password === 'pwd') {
		req.session.user = { name: req.body.username }
		res.redirect('/')
		next()
		return
	}

	res.render('login', { fail: true })
	next()
})

router.get('/logout', (req, res) => {
	req.session.user = null
	res.redirect('/')
})

module.exports = router
```

When the authentication is successful, we set the `req.session.user` value to the supplied `username` and redirect the authenticated user back to the `/` endpoint. At this point, the `express-session` middleware creates a session identifier and sets the `Set-Cookie` ==**HTTP**== ==header== on the request. The key name will default to `connect.sid`. We override this value with `SESSIONID` to avoid the ==fingerprinting== of our server ( ff we left the default value, the attacker could easily infer from this ==header== that we're using **Express.js** with the `express-session` middleware)

> [!important] The
> 
> `Set-Cookie` header is set to the session key name and session identifier.

The `express-session` middleware defaults to using an ==in-process storage mechanism== to store the ==session tokens==. However, these tokens are ==not expired==, which means our process will continue to be ==populated== with more and more tokens. This could eventually result in ==degraded performance== or ==crash== our process.

### Securing session cookies

Session cookies can be marked with a `Secure` attribute. The `Secure` attribute forces the browser to not use ==**HTTP**== to send cookies back to the server. This is to avoid ==**Man-In-The-Middle (MITM)**== attacks.

In production applications, ==**HTTPS**== and `secure cookies` should be used. But in development, it's easier to use ==**HTTP**==.

### Hashing with `bcrypt`

> [!important] **Passwords**
> 
> should ==never== be stored in ==plain text== and should instead be stored in a ==hashed form==.

[`bcrypt`](https://www.npmjs.com/package/bcrypt) is a popular module that is used to hash passwords in [[NodeJS]]

```JavaScript
const bcrypt = require('bcrypt')
const password = process.argv[2]

const saltRounds = 10

bcrypt.hash(password, saltRounds, (err, hash) => {
	if (err) throw err
	console.log(hash)
})
```

---

## Securing HTTP headers with `helmet`

> [!info] Helmet.js  
> Helmet helps secure Express apps by setting HTTP response headers.  
> [https://helmetjs.github.io/](https://helmetjs.github.io/)  

**Express.js** is a ==lightweight== web framework, so certain measures that are typically taken to better secure applications are ==not implemented== by the core framework. One of the precautionary measures we can take is to set certain security-related ==**HTTP**== ==headers== on requests.

```JavaScript
const express = require('express')
const helmet = require('helmet')

const app = express()
app.use(helmet())
app.get('/', (req, res) => res.send('Hello World!'))
app.listen(3000, () => {
	console.log('Server listening on port 3000')
})
```

```Bash
curl -I http://localhost:3000
```

  

![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled 3.png|Untitled 3.png]]

  

`helmet` removes the `X-Powered-By: Express` header so that discovering the server is _Express-based_ becomes more difficult. The reason to obfuscate this is to protect against attackers trying to exploit ==Express.js-oriented security vulnerabilities==, slowing them down in determining the type of server being used in the application.

---

## Protecting against ==HTTP== parameter pollution attacks

One of the easiest groups of vulnerabilities to exploit is ==injection attacks==, with ==SQL injection attacks== being the most common. ==SQL injection attacks== are where an attacker injects ==malicious SQL== into an application to _delete_, _distort_, or _expose_ `data` stored in the database.

==Parameter pollution== is a type of injection attack where the ==**HTTP**== ==parameters== of a web application's HTTP endpoints are injected with specific ==malicious input==. ==**HTTP**== ==parameter pollution== can be used to _expose_ internal data or even cause a ==**Denial of Service (DoS)**== ==attack==, where an attacker tries to ==interrupt== a resource and ==render it inaccessible== by the resource's intended users.

```JavaScript
const express = require('express')
const app = express()

app.get('/', (req, res) => {
	asyncWork(() => {
		const upper = (req.query.msg || '').toUpperCase() + '\n'
		res.send(upper)
	})
})
asyncWork = (callback) => {
	setTimeout(callback, 0)
}
app.listen(3000, () => {
	console.log('Server listening on port 3000')
})
```

```Bash
curl http://localhost:3000/\?msg\=hello\&msg\=world
```

  

We can see that the server has ==crashed== with the following error

  

![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled 4.png|Untitled 4.png]]

---

  

It is possible to cause the server to crash just by sending ==duplicate parameters==. This makes it fairly easy for a perpetrator to launch an effective ==**DoS**== ==attack==.

  

```Bash
		let msg = req.query.msg
		if (Array.isArray(msg)) msg = msg.pop()
```

  

---

## Preventing ==JSON== pollution

The ==**JavaScript**== language allows all `Object` ==attributes== to be altered. In a ==**JSON**== pollution attack, an attacker leverages this ability to ==override built-in== _attributes_ and _functions_ with malicious code.

Applications that accept ==**JSON**== as user input are the most susceptible to these attacks.

In the most severe cases, it's possible to crash a server by just supplying ==additional values== in ==**JSON**== input. This can make the server vulnerable to **==DoS==** ==attacks== via ==**JSON**== pollution.

```JavaScript
const http = require('http')
const { STATUS_CODES } = http
const server = http.createServer((req, res) => {
	if (req.method === 'POST' && req.url === '/') {
		greeting(req, res)
		return
	}
	res.statusCode = 404
	res.end(STATUS_CODES[res.statusCode])
})

greeting = (req, res) => {
	let data = ''
	req.on('data', (chunk) => (data += chunk))
	req.on('end', () => {
		try {
			data = JSON.parse(data)
		} catch (e) {
			res.end('')
			return
		}
		if (data.hasOwnProperty('name')) { // vulnerable
			res.end(`${data.msg} ${data.name}`)
		} else {
			res.end(data.msg)
		}
	})
}
server.listen(3000, () => {
	console.log('Server listening on port 3000')
})
```

```Bash
curl -H "Content-Type: application/json" -X POST -d '{"msg": "Hello", "name": "Beth" }' http://localhost:3000/
```

---

When we try altering the payload to send an additional ==**JSON**== property named `hasOwnProperty`

  

```Bash
curl -H "Content-Type: application/json" -X POST -d '{"msg": "Hello", "name": "Beth", "hasOwnProperty" : 0 }' http://localhost:3000/
```

  

It has ==crashed== with the following error

![[Notion/Class Notes/NodeJS/Node.js securing/attachments/Untitled 5.png|Untitled 5.png]]

It’s because the `hasOwnProperty()` function has been ==overridden== by the `hasOwnProperty` value in the ==**JSON**== input.

  

We can protect against this by validating our ==**JSON**== input using the `ajv` module.

```JavaScript
const Ajv = require('ajv')
const ajv = new Ajv()
const schema = {
	title: 'Greeting',
	properties: {
		msg: { type: 'string' },
		name: { type: 'string' },
	},
	additionalProperties: false,
	required: ['msg'],
}

const validate = ajv.compile(schema)

greeting = (req, res) => {
	...
	if(!validate(data, schema) {
		res.end('Invalid JSON inputs')
		return()
	}
	...
}
```

---

## Preventing Cross-Site Scripting attacks

==**XSS**== ==attacks== are ==client-side injection== attacks where malicious scripts are injected into websites. ==**XSS**== ==vulnerabilities== are ==_very dangerous_==, as they can compromise trusted websites.

```JavaScript
const express = require('express')
const app = express()
app.get('/', (req, res) => {
	const { previous, lang, token } = req.query
	getServiceStatus((status) => {
		res.send(`
      <h1>Service Status</h1>
      <div id=status>
        ${status}
      </div>
      <div>
        <a href="${previous}${token}/${lang}">Back</a>
      </div>
    `)
	})
})

getServiceStatus = (callback) => {
	const status = 'All systems are running.'
	callback(status)
}

app.listen(3000, () => {
	console.log('Server listening on port 3000')
})
```

Now, we can craft an ==**XSS**== ==attack==. We will craft a **URL** that will inject `parameters`

We're aiming to inject the following ==**JavaScript**== via the **URL** parameters `document.getElementById("status").innerHTML="All systemsare down!"`

```Bash
http://localhost:3000/?previous=%22%3E%3Cscri&token=pt%3Edocument.getElementById(%22status%22).innerHTML=%22All%20systems%20are%20down!%22;%3C&lang=script%3E%20%3Ca%20href=%22/
```

Now, the web page will show `All systems are down!`. So, ==visitors== to our legitimate service status page will see a ==malicious message==.

---

To fix the application, we need to ==escape== or ==sanitize== the inputs by using a module named `he`

```JavaScript
const href = require('he').encode(`${previous}${token}/${lang}`);

...
	<a href="${href}">Back</a>
...
```

  

So when we try to craft a **URL** which inject the ==**JavaScript**== scripts again. The injection attack no longer works!

We've used the `he` module to prevent an ==**XSS**== ==attack==

  

==**XSS**== ==attacks== are ==client-side injection attacks== where ==malicious scripts== are injecting into trusted websites. The general flow of an ==**XSS**== ==attack== is as follows:

1. Malicious input enters the application – typically via a ==web request==.
2. The input is rendered as dynamic content on the web page because the input has ==not== been ==appropriately sanitized==.

> [!important] We can use
> 
> ==**Node.js**=='s `decodeURI()` method to decode ==encoded URIs==

---

## Guarding against Cross-Site Request Forgery attacks

==**CSRF**== is an attack where a malicious web application causes a ==user's web browser== to execute an action on ==another trusted web application== where the user is logged in

> [!important] Browser security has
> 
> ==improved== significantly in recent years. It's very difficult to replicate a ==**CSRF**== attack on any ==modern browser.== However, as there are still many users on ==older browsers==, it's important to understand how these  
> attacks work and how to protect against them.