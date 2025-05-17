
> *One of the main attractions to **Node.js** is the massive ecosystem of external third-party libraries. **Node.js** modules are libraries or a set of functions you want to include in your application.*
> 

## `nvm`

It is recommended to install **Node.js** with *Node Version Manager* (`nvm`). It is a tool that enables you to easily switch **Node.js** versions on most Unix-like platforms.

[https://github.com/nvm-sh/nvm.git](https://github.com/nvm-sh/nvm.git)

---

## `npm`

`npm` is the name of the *Command-Line Interface* tool (**CLI**) bundled with **Node.js** as the default package manager.

[https://github.com/npm/npm.git](https://github.com/npm/npm.git)

---

## `yarn`

`yarn` is a popular alternative package manager for JavaScript and was created as an alternative to the `npm` **CLI** in 2016. When Yarn was released, `npm` did not have the `package-lock.json` feature to guarantee consistency of which specific versions of modules would be installed. This was one of the key features of `yarn`

[Home page | Yarn](https://yarnpkg.com/)

---

## Preparing and publishing your module to `npm`

### How to do it

1. Once you have signed up for an [`npm`](https://npmjs.com) account, you can authorize your `npm` client with the following command
    
    ```bash
    npm login
    Username: liemnguyen.example
    Password:
    Email: (this IS public) liemnguyen.exmaple@vn.ibm.com
    ```
    
2. Let's update our [README.md](http://readme.md/) file that was automatically created for us when we initialized the **GitHub** repository
    
    ```markdown
    # reverse-sentence
    Reverses the words of a sentence.
    ## Install
    ```sh
    npm install @npmusername/reverse-sentence
    ```
    ## API
    ```js
    require("reverse-sentence") => Function
    reverse(sentence) => String
    ```
    ## Example
    ```js
    const reverseSentence = require("reverse-sentence");
    const sentence = "Hello Beth!";
    const reversed = reverseSentence(sentence);
    console.log(reversed) // Beth! Hello
    ```
    ## License
    MIT
    ```
    
3. Now, we need to update the name of our module in the `package.json` file to match our scoped module name.
    
    ```json
    {
    	"name": "@npmusername/reverse-sentence",
    	"version": "0.1.0",
    	"description": "Reverses a sentence."
    	...
    }
    ```
    
4. It is ideal to keep your public **GitHub** repository up to date. Typically, module authors will create a "tag" on GitHub that matches the version that is pushed to `npm`.
    
    ```bash
    git push origin master
    git tag v0.1.0
    git push origin v0.1.0
    ```
    
5. Now we're ready to publish our module to the `npm` registry using the following command
    
    ```bash
    npm publish --access=public
    ```
    

### `.npmignore`

Similar to a .`gitignore` file, which specifies which files should not be tracked or committed to a repository, `.npmignore` omits the files listed in it from the package. `.npmignore` files are not mandatory, and if you do not have one but do have a `.gitignore` file, then `npm` will omit the files and directories matched by the `.gitignore` file. The `.npmignore` file will override `.gitignore` if one exists.

---

## Using ECMAScript modules

**ECMAScript** is the language specification created to standardize **JavaScript**, defined by *ECMAScript International*. **ECMAScript** modules are the official format to package **JavaScript** code for reuse.

```jsx
import express from 'express'
import { name } from './get-name/index.mjs'

const PORT = 3000
const app = express()

app.get('/', (req, res) => res.send(`Hello from ${name}`))

app.listen(PORT, () => {
	console.log('Express listening on port: ' + PORT)
})
```

`mjs` is the extension for **ECMAScript** module files. This file ending indicates that **Node.js** should treat the file as an **ECMAScript** module. There's another ending, `.cjs`; **Node.js** always treats files with this ending as **CommonJS** modules.

There are other ways of indicating that you'd like to treat a module as an **ECMAScript** module. Files ending in `.js` are treated as **ECMAScript** modules

```json
{
	...
	"type" : "module",
	...
}
```