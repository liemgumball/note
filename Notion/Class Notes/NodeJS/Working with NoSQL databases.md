> ==**_NoSQL_**== _database that focuses on high performance and availability._

## Target

- Connecting and persisting to ==**MongoDB**==

---

> [!important]
> 
> [[MongoDB]] is a popular ==**NoSQL**== database which provide a ==**SQL**==-like syntax.

## Connecting and persisting to ==MongoDB==

```JavaScript
const { MongoClient } = require('mongodb')

const task = process.argv[2]

const URL = 'mongodb://localhost:27017'
const client = new MongoClient(URL)

async function main() {
	// Use connect method to connect to the server
	await client.connect()
	console.log('Connected successfully to server')

	const tasks = client.db('tasklist').collection('tasks')

	if (task) {
		const result = await tasks.insertOne({ task: task })
		console.log('Inserted task: ', result)
	}
	;(await tasks.find({}).toArray()).forEach((task) => console.log(task))

	return 'done.'
}

main()
	.then(console.log)
	.catch(console.error)
	.finally(() => client.close())
```

We imports the `MongoClient` class from the `mongodb` module. This class represents and exposes methods to create a client `connection` to a ==**MongoDB**== database.

> [!important] ==**MongoDB**==
> 
> sets the ==last== document to `null` by default, to note that it is the end of the collection.

---

If we want to add schemas to your ==**MongoDB**== data to enable you to model your application data. An `npm` module named `mongoose` provides object modeling for ==**MongoDB**==. Let's take a look at how we can model an application using `mongoose`.

### ==Mongoose==

**==Mongoose==** is an ==object data modeling== library that enables you to apply schemas to ==**MongoDB**== data with [[NodeJS]] . It saves us from having to manually validate your document objects

```JavaScript
const mongoose = require('mongoose')

const URL = 'mongodb://localhost:27017/customers'

mongoose.connect(URL, {})

const Customer = mongoose.model('Customer', {
	forename: String,
	surname: String,
})

const customer1 = new Customer({
	forename: 'Liem',
	surname: 'Nguyen',
})

customer1.save().then((doc) => {
	console.log('Added new customer:', doc.forename, doc.surname)
	listCustomers()
})

function listCustomers() {
	console.log('Customers:')
	Customer.find().then((doc) => {
		doc.forEach((customer) => {
			console.log(`- ${customer.surname}, ${customer.forename}`)
			mongoose.connection.close()
		})
	})
}
```