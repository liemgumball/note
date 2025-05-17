Created: February 19, 2024 3:17 PM
Class: Agility IO InternShip
Type: Back-end
Materials: https://www.mongodb.com/, https://www.w3schools.com/mongodb/index.php, https://mongodb.github.io/node-mongodb-native/6.3/modules.html
Reviewed: No
Edited: May 10, 2025 2:46 PM

# MongoDB

<aside>
💡 It’s a document database. It stores data in a type of **JSON** format called **BSON**

</aside>

## A MongoDB document

A record in **MongoDB** is a document, which is a data structure composed of field and value pairs. **MongoDB** documents are similar to **JSON** objects. The values of fields may include other `documents`, `arrays`, and `documents[]`.

```json
{
	title: "Post Title 1",
	body: "Body of post.",
	category: "News",
	likes: 1,
	tags: ["news", "events"],
}
```

The advantages of using `documents` are:

- Documents correspond to native data types in many programming languages
- Embedded documents and arrays reduce need for expensive joins
- Dynamic schema supports fluent polymorphism

## SQL vs Document Databases

| **SQL** | **MongoDB** |
| --- | --- |
| Databases are considered relational databases | Document database which is often referred to as a non-relational database *(this does not mean that relational data cannot be stored in document databases. It means that relational data is stored differently. A better way to refer to it is as a non-tabular database.)* |
| Store related data in separate tables | Stores data in flexible documents. Instead of having multiple tables you can simply keep all of your related data together. This makes reading your data very fast. |
| When data is needed, it is queried from multiple tables to join the data back together | Still have multiple groups of data too. Instead of tables these are called [Collections](MongoDB.md)  |

---

## Collections

**Collections** are analogous to tables in relational databases. If a collection does not exist, **MongoDB** creates the collection when we first store data for that collection

## Node module reference

[mongodb](https://mongodb.github.io/node-mongodb-native/6.3/modules.html)

## Query API

The [MongoDB Query API](https://www.mongodb.com/docs/manual/query-api/?utm_campaign=w3schools_mdb&utm_source=w3schools&utm_medium=referral) is the way we will interact with data.

The Query API comprises two ways to query data in **MongoDB**:

- [CRUD Operations](https://www.mongodb.com/docs/manual/crud/#std-label-crud)
- [Aggregation pipelines](https://www.mongodb.com/docs/manual/core/aggregation-pipeline/#std-label-aggregation-pipeline)

### `mongosh` (Mongo Shell)

[Install mongosh](https://www.mongodb.com/docs/mongodb-shell/install/?utm_campaign=w3schools_mdb&utm_source=w3schools&utm_medium=referral)

Quick reference

[Quick Reference](https://www.mongodb.com/docs/drivers/node/current/quick-reference/#std-label-node-quick-reference)

## CRUD Operations with [NodeJS](NodeJS.md)

### Show all database

```bash
show dbs
```

### Change or create database

```bash
use blog
```

### Create Collection

1. Create a collection using the `createCollection()` database method.
    
    ```bash
    db.createCollection('posts')
    ```
    
2. Create a collection during the `insert` process.
    
    ```bash
    db.posts.insertOne(object)
    ```
    

---

### Insert `document`

1. `insertOne()`
    
    ```bash
    db.posts.insertOne({
      title: "Post Title 1",
      body: "Body of post.",
      category: "News",
      likes: 1,
      tags: ["news", "events"],
      date: Date()
    })
    ```
    
2. `insertMany()`
    
    ```bash
    db.posts.insertMany([  
      {
        title: "Post Title 2",
        body: "Body of post.",
        category: "Event",
        likes: 2,
        tags: ["news", "events"],
        date: Date()
      },
      {
        title: "Post Title 3",
        body: "Body of post.",
        category: "Technology",
        likes: 3,
        tags: ["news", "events"],
        date: Date()
      },
      {
        title: "Post Title 4",
        body: "Body of post.",
        category: "Event",
        likes: 4,
        tags: ["news", "events"],
        date: Date()
      }
    ])
    ```
    

---

### Find `document`

1. `find()`
    
    ```bash
    db.posts.find()
    ```
    
2. `findOne()`
    
    ```bash
    db.posts.findOne()
    ```
    

### Query `document`

```bash
db.posts.find( {category: "News"} )
```

- Projection
    
    Both `find` methods accept a second parameter called `projection`.
    
    This parameter is an `object` that describes which fields to include in the results.
    
    ```bash
    db.posts.find({}, {title: 1, date: 1})
    ```
    
    <aside>
    💡 **Note:** This parameter is optional. If omitted, all fields will be included in the results.
    The `_id` field is also included. This field is always included unless specifically excluded below
    
    </aside>
    
    ```bash
    db.posts.find({}, {_id: 0, title: 1, date: 1})
    ```
    
    We can exclude the date category field. All other fields will be included in the results.
    
    ```bash
    db.posts.find({}, {category: 0})
    ```
    
    <aside>
    📌 We will get an error if we try to specify both 0 and 1 in the same object.
    
    </aside>
    
    ```bash
    db.posts.find({}, {title: 1, date: 0})
    ```
    

---

### Update `document`

1. `updateOne()`
    
    The method will update the first document that is found matching the provided query. 
    
    ```bash
    db.posts.updateOne( { title: "Post Title 1" }, { $set: { likes: 2 } } )
    ```
    
    <aside>
    📌 **Insert if not found**
    The method will insert the document if it is not found, by use the `upsert` option.
    
    </aside>
    
    ```bash
    db.posts.updateOne( 
      { title: "Post Title 5" }, 
      {
        $set: 
          {
            title: "Post Title 5",
            body: "Body of post.",
            category: "Event",
            likes: 5,
            tags: ["news", "events"],
            date: Date()
          }
      }, 
      { upsert: true }
    )
    ```
    
2. `updateMany()`
    
    The method will update all documents that match the provided query.
    
    ```bash
    db.posts.updateMany({}, { $inc: { likes: 1 } })
    ```
    

---

### Update Arrays in a `document`

1. Positional Operator [`$`](https://www.mongodb.com/docs/drivers/node/current/fundamentals/crud/write-operations/embedded-arrays/#the-first-matching-array-element)
This method update the first array element of each `document` that matches the query
    
    ```jsx
    /* Data
    	{
    	  _id: ...,
    	  entries: [
    	    { x: false, y: 1 },
    	    { x: "hello", y: 100 },
    	    { x: "goodbye", y: 1000 }
    	  ]
    	}
    */
    
    // Query for all elements in entries array where the value of x is a string
    const query = { "entries.x": { $type : "string" } }
    
    // On first matched element, increase value of y by 33
    const updateDocument = {
      $inc: { "entries.$.y": 33 }
    }
    
    // Execute the update operation
    const result = await myColl.updateOne(query, updateDocument)
    
    /* Updated
    	{
    	  _id: ...,
    	  entries: [
    	    { x: false, y: 1 },
    	    { x: "hello", y: 100 },
    	    { x: "goodbye", y: 1000 }
    	  ]
    	}
    */
    ```
    
2. All Positional Operator [`$[]`](https://www.mongodb.com/docs/drivers/node/current/fundamentals/crud/write-operations/embedded-arrays/#matching-all-array-elements)
    
    This method perform the update on all of the array elements of each `document` that matches the query
    
    ```jsx
    /* Data
    	{
    	  _id: ...,
    	  date: "5/15/2023",
    	  calls: [
    	    { time: "10:08 am", caller: "Mom", duration: 67 },
    	    { time: "4:11 pm", caller: "Dad", duration: 121 },
    	  ]
    	}
    */
    
    // Query for all documents where date is the string "5/15/2023"
    const query = { date: "5/15/2023" };
    // For each matched document,
    // remove duration field from all entries in calls array 
    const updateDocument = {
      $unset: { "calls.$[].duration": "" }
    };
    // Execute the update operation
    const result = await myColl.updateOne(query, updateDocument);
    
    /* Updated
    	{
    	  _id: ...,
    	  date: "5/15/2023",
    	  calls: [
    	    { time: "10:08 am", caller: "Mom", duration: 67 },
    	    { time: "4:11 pm", caller: "Dad", duration: 121 },
    	  ]
    	}
    */
    ```
    
3. Filtered Positional Operator [`$[<identifier>]`](https://www.mongodb.com/docs/drivers/node/current/fundamentals/crud/write-operations/embedded-arrays/#matching-multiple-array-elements)
    
    This method perform an update on all embedded array elements of each `document` that matches your query
    
    ```jsx
    /* Data
    	{
    	  _id: ...,
    	  date: "11/12/2023",
    	  items: [
    	    { item: "Scallions", quantity: 3, recipe: "Fried rice" },
    	    { item: "Mangos", quantity: 4, recipe: "Salsa" },
    	    { item: "Pork shoulder", quantity: 1, recipe: "Fried rice" },
    	    { item: "Sesame oil", quantity: 1, recipe: "Fried rice" }
    	  ]
    	}
    */
    
    // Query for all documents where date is the string "11/12/2023"
    const query = { date: "11/12/2023" };
    // For each matched document, change the quantity of items to 2 
    const updateDocument = {
      $mul: { "items.$[i].quantity": 2 }
    };
    // Update only non-oil items used for fried rice 
    const options = {
      arrayFilters: [
        {
          "i.recipe": "Fried rice",
          "i.item": { $not: { $regex: "oil" } },
        }
      ]
    };
    // Execute the update operation
    const result = await myColl.updateOne(query, updateDocument, options);
    
    /* Updated
    	{
    	  _id: ...,
    	  date: "11/12/2023",
    	  items: [
    // matched  { item: "Scallions", quantity: 6, recipe: "Fried rice" }, 
    	          { item: "Mangos", quantity: 4, recipe: "Salsa" },
    // matched  { item: "Pork shoulder", quantity: 2, recipe: "Fried rice" },
    	          { item: "Sesame oil", quantity: 1, recipe: "Fried rice" }
    	  ]
    	}
    */tra
    ```
    

---

### Delete `document`

1. `deleteOne()`
    
    The method will delete the first document that matches the query provided.
    
    ```bash
    db.posts.deleteOne({ title: "Post Title 1" })
    ```
    
2. `deleteMany()`
    
    The method will delete all documents that match the query provided.
    
    ```bash
    db.posts.deleteMany({ category: "Technology" })
    ```
    

---

### **Query Operators**

There are many query operators that can be used to compare and reference document fields.

- Comparison
    - `$eq`: Values are equal
    - `$ne`: Values are not equal
    - `$gt`: Value is greater than another value
    - `$gte`: Value is greater than or equal to another value
    - `$lt`: Value is less than another value
    - `$lte`: Value is less than or equal to another value
    - `$in`: Value is matched within an array
- Logical
    - `$and`: Returns documents where both queries match
    - `$or`: Returns documents where either query matches
    - `$nor`: Returns documents where both queries fail to match
    - `$not`: Returns documents where the query does not match
- Evaluation
    - `$regex`: Allows the use of regular expressions when evaluating field values
    - `$text`: Performs a text search
    - `$where`: Uses a JavaScript expression to match documents

### Update Operators

- Fields
    - `$currentDate`: Sets the field value to the current date
    - `$inc`: Increments the field value
    - `$rename`: Renames the field
    - `$set`: Sets the value of a field
    - `$unset`: Removes the field from the document
- Array
    - `$addToSet`: Adds distinct elements to an array
    - `$pop`: Removes the first or last element of an array
    - `$pull`: Removes all elements from an array that match the query
    - `$push`: Adds an element to an array

### `bulkWrite()` **Operations**

This method performs batch write operations against a *single* collection. This method reduces the number of network round trips from your application to the server which therefore increases the throughput and performance. Bulk writes return a collection of results for all operations only after *all* operations passed to the method complete.

We can specify one or more of the following write operations in `bulkWrite()`:

- `insertOne`
- `updateOne`
- `updateMany`
- `deleteOne`
- `deleteMany`
- `replaceOne`

```jsx
const database = client.db("sample_mflix");
    const theaters = database.collection("theaters");

    // Insert a new document into the "theaters" collection
    const result = await theaters.bulkWrite([
      {
        insertOne: {
          document: {
            location: {
              address: {
                street1: "3 Main St.",
                city: "Anchorage",
                state: "AK",
                zipcode: "99501",
              },
            },
          },
        },
      },

      {
        insertOne: {
          document: {
            location: {
              address: {
                street1: "75 Penn Plaza",
                city: "New York",
                state: "NY",
                zipcode: "10001",
              },
            },
          },
        },
      },

      {
        // Update documents that match the specified filter
        updateMany: {
          filter: { "location.address.zipcode": "44011" },
          update: { $set: { is_in_ohio: true } },
          upsert: true,
        },
      },

      {
        // Delete a document that matches the specified filter
        deleteOne: { filter: { "location.address.street1": "221b Baker St" } },
      },
    ]);

    // Log the result of the bulk write operation 
    console.log(result);
```

---

## Aggregation Pipelines with [NodeJS](NodeJS.md)

<aside>
💡 **Aggregation operations** allow to `*group*`, `*sort*`, `*perform calculations*`, `*analyze data*`, and much more

</aside>

**Aggregation pipelines** can have one or more "stages". The order of these stages are important. Each stage acts upon the results of the previous stage.

```bash
db.posts.aggregate([
  // Stage 1: Only find documents that have more than 1 like
  {
    $match: { likes: { $gt: 1 } }
  },
  // Stage 2: Group documents by category and sum each categories likes
  {
    $group: { _id: "$category", totalLikes: { $sum: "$likes" } }
  }
])
```

### `$group`

This aggregation stage groups `documents` by the unique `_id` expression provided.

<aside>
⚠️ Don't confuse this `_id` expression with the `_id` ObjectId provided to each `document`

</aside>

```bash
db.posts.aggregate([ { $group: { _id: '$category' } } ])

# [ { _id: 'Event' }, { _id: 'Technology' } ]
```

### `$limit`

This aggregation stage limits the number of `documents` passed to the next stage.

```bash
db.posts.aggregate([ { $limit: 1} ])
```

### `$project`

This aggregation stage passes only the specified fields along to the next aggregation stage.

<aside>
💡 This is the same projection that is used with the [Projection](MongoDB%20aaf063179c2744b0a6ddfeccc967b3cf.md) method.

</aside>

```bash
db.restaurants.aggregate([
  {
    $project: {
      name: 1,
      cuisine: 1,
      address: 1
    }
  },
  {
    $limit: 5
  }
])
```

### `$sort`

This aggregation stage groups sorts all `documents` in the specified sort order.

<aside>
📌 Remember that the order of stages matters. Each stage only acts upon the documents that previous stages provide.

</aside>

```bash
db.posts.aggregate([ 
  { 
    $sort: { likes: -1 } # as decsending
  },
  {
    $project: {
      title: 1, # as acsending
      category: 1
    }
  },
  {
    $limit: 5
  }
])
```

### `$match`

This aggregation stage behaves like a `find`. It will filter `documents` that match the query provided.

```bash
db.posts.aggregate([
	{
		$match: { likes: { $gt:1 } }
	},
	{
		$limit: 5
	}
])
```

<aside>
📌 Using `$match` early in the pipeline can improve performance since it limits the number of `documents` the next stages must process.

</aside>

### `$addField`

This aggregation stage adds new fields to `documents`

```bash
db.restaurants.aggregate([
  {
    $addFields: {
      avgGrade: { $avg: "$grades.score" } # as average of all grades.score
    }
  },
  {
    $project: {
      "name": 1,
      "avgGrade": 1
    }
  },
  {
    $limit: 5
  }
])
```

### `$count`

This aggregation stage counts the total amount of `documents` passed from the previous stage.

```bash
db.posts.aggregate([
  {
    $match: { category: "Event" }
  },
  {
    $count: "totalEvent"
  }
])
```

### `$lookup`

This aggregation stage performs a left outer join to a `collection` in the same database.

There are four required fields:

- `from`: The collection to use for lookup in the same database
- `localField`: The field in the primary collection that can be used as a unique identifier in the `from` collection.
- `foreignField`: The field in the `from` collection that can be used as a unique identifier in the primary collection.
- `as`: The name of the new field that will contain the matching documents from the `from` collection.

```bash
db.comments.aggregate([
  {
    $lookup: {
      from: "posts",
      localField: "post_id",
      foreignField: "_id",
      as: "post_details",
    },
  },
  {
    $limit: 1
  }
])
```

### `$out`

This aggregation stage writes the returned `documents` from the aggregation pipeline to a `collection`

```bash
db.listingsAndReviews.aggregate([
  {
    $group: {
      _id: "$property_type",
      properties: {
        $push: {
          name: "$name",
          accommodates: "$accommodates",
          price: "$price",
        },
      },
    },
  },
  { $out: "properties_by_type" },
])
```

<aside>
📌 The `$out` stage must be the last stage of the aggregation pipeline.

</aside>

### **Access Data From a `cursor`**

[Access Data From a Cursor](https://www.mongodb.com/docs/drivers/node/current/fundamentals/crud/read-operations/cursor/)

The following functions directly return `cursor`

- `Collection.find()`
- `Collection.aggregate()`
- `Collection.listIndexes()`
- `Collection.listSearchIndexes()`
- `Db.aggregate()`
- `Db.listCollections()`

There are many ways the iterate through data with `cursor`

- **Asynchronous Iteration**
    
    ```jsx
    for await ( const doc in cursor ){
    	console.log(doc)
    }
    ```
    
- **Manual Iteration**
    
    ```jsx
    while( await cursor.hasNext() ){
    	console.log(await cursor.next())
    }
    ```
    
- **Return to Array of All `document`** *(Note that large numbers of matched documents can cause performance issues or failures if the operation exceeds memory constraints)*
    
    ```jsx
    const array = await cursor.toArray() // not recommened
    ```
    
- **Stream API** `stream()`
    
    ```jsx
    cursor.stream().on('data', doc => { console.log(doc) })
    ```
    
- **Event API**
    
    ```jsx
    cursor.on('data', doc => { console.log(doc) })
    ```
    

---

## Session & Transaction

Transactions allow us to run a series of operations that do not change any data until the entire transaction is committed

In **MongoDB**, multi-document transactions run within a **client session**. A client session is a grouping of related *read* or *write* operations that you want to execute sequentially

[Transactions](https://www.mongodb.com/docs/drivers/node/current/fundamentals/transactions/#)

<aside>
💡 It’s recommend you reuse your client for multiple sessions and transactions instead of instantiating a new client each time

</aside>

```jsx
async function coreTest(client) {
  const session = client.startSession();
  try {
    session.startTransaction();

		// withdraw
    const savingsColl = client.db("bank").collection("savings_accounts");
    await savingsColl.findOneAndUpdate(
      {account_id: "9876"}, 
      {$inc: {amount: -100 }}, 
      { session });
		
		// deposit
    const checkingColl = client.db("bank").collection("checking_accounts");
    await checkingColl.findOneAndUpdate(
      {account_id: "9876"}, 
      {$inc: {amount: 100 }}, 
      { session });

    // ... perform other operations

    await session.commitTransaction();
    console.log("Transaction committed.");
  } catch (error) {
    console.log("An error occurred during the transaction:" + error);
    await session.abortTransaction();
  } finally {
    await session.endSession();
  }
}
```

<aside>
<img src="https://www.notion.so/icons/exclamation-mark_red.svg" alt="https://www.notion.so/icons/exclamation-mark_red.svg" width="40px" /> **Use a Session with the Client That Started It**

The driver throws an error if you provide a session from one `MongoClient` instance to a different client instance

</aside>

There are some **Convenient Transaction API**

- `withSession()`
- `withTransaction()`

```jsx
async function convTest(client) {
  let txnRes = await client.withSession(async (session) =>
    session.withTransaction(async (session) => {
      const savingsColl = client.db("bank").collection("savings_accounts");
      await savingsColl.findOneAndUpdate(
        {account_id: "9876"}, 
        {$inc: {amount: -100 }}, 
        { session });
  
      const checkingColl = client.db("bank").collection("checking_accounts");
      await checkingColl.findOneAndUpdate(
        {account_id: "9876"}, 
        {$inc: {amount: 100 }}, 
        { session });

      // ... perform other operations

      return "Transaction committed.";
    }, null)
  );
  console.log(txnRes);
}
```

---

## Indexes in MongoDB

[Indexes](https://www.mongodb.com/docs/drivers/node/current/fundamentals/indexes/)

[Indexing](Indexing.md)

<aside>
💡 Without indexes, **MongoDB** must scan *every* `document` in a `collection` to find the documents that match each query. These `collection` scans are slow and can negatively affect the performance of your application. By using an index to limit the number of documents **MongoDB** scans, queries can be more efficient and therefore return faster

</aside>

```jsx
// List the indexes on the collection and output them as an array
const result = await collection.listIndexes().toArray();

// Print the list of indexes
console.log("Existing indexes:\n");
for(const doc in result){
    console.log(doc);
}
```

For example:

Instead of scan through each individual `document` and look into their field to find where is `rating` has value `10` . It may not very efficient, so the `index` created like an pointer which knowing exactly where the `document` has `rating: 10`. 

![Untitled](Notion/Class%20Notes/MongoDB/Untitled.png)

<aside>
📌 **Note:** We don’t have to create `index` for every field of data. When we add a new `document` to the `collection` , the `index` have to update its self to match that change.

</aside>

## MongoDB validation

### Schema validation

By default **MongoDB** has a flexible schema. This means that there is no strict schema validation set up initially. Schema validation rules can be created in order to ensure that all `documents` a collection share a similar structure.

```jsx
db.createCollection("posts", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: [ "title", "body" ],
      properties: {
        title: {
          bsonType: "string",
          description: "Title of post - Required."
        },
        body: {
          bsonType: "string",
          description: "Body of post - Required."
        },
        category: {
          bsonType: "string",
          description: "Category of post - Optional."
        },
        likes: {
          bsonType: "int",
          description: "Post like count. Must be an integer - Optional."
        },
        tags: {
          bsonType: ["string"],
          description: "Must be an array of strings - Optional."
        },
        date: {
          bsonType: "date",
          description: "Must be a date - Optional."
        }
      }
    }
  }
})
```

---

## Mongoose

[Mongoose](Mongoose.md)