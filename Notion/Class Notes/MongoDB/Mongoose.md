> [!important] ==**Mongoose**==
> 
>  is one of the most powerful external module of the ==**Node.js**==  
> ==**Mongoose**== is a ==**MongoDB**== ==**ODM**== _(Object database Modelling)_ that is used to translate the code and its representation from [[MongoDB]] to the ==**Node.js**== server

> [!info] Mongoose v8.2.0: Schemas  
> If you haven't yet done so, please take a minute to read the quickstart to get an idea of how Mongoose works.  
> [https://mongoosejs.com/docs/guide.html](https://mongoosejs.com/docs/guide.html)  

---

## Schemas

Everything in ==**Mongoose**== starts with a ==**Schema**==. Each schema maps to a ==**MongoDB**== `collection` and defines the shape of the `documents` within that `collection`

```JavaScript
import mongoose from 'mongoose'
const { Schema } = mongoose

const blogSchema = new Schema({
	title: String, // String is shorthand for {type: String}
	author: String,
	body: String,
	comments: [{ body: String, date: Date }],
	date: { type: Date, default: Date.now },
	hidden: Boolean,
	meta: {
		votes: Number,
		favs: Number,
	},
})
```

The permitted ==**SchemaTypes**== are

- `String`
- `Number`
- `Date`
- `Buffer`
- `Boolean`
- `Mixed`
- `ObjectId`
- `Array`
- `Decimal128`
- `Map`
- `UUID`

### Creating Model

This will create a ==lowercase collection== in ==**MongoDB**==

```JavaScript
const Blog = mongoose.model('Blog', blogSchema);
```

By default, ==**Mongoose**== adds an `_id` property to our ==schemas==

```JavaScript
const schema = new Schema();

schema.path('_id'); // ObjectId { ... }
```

We can also overwrite Mongoose's default `_id` with our own `_id`

> [!important] **Just be careful**
> 
>   
>   
> ==**Mongoose**== will refuse to save a top-level document that doesn't have an `_id`, so we’re responsible for setting `_id` if you define your own `_id` path.  
> ==**Mongoose**== also adds an `_id` property to `subdocuments`

```JavaScript
const nestedSchema = new Schema(
  { name: String },
  { _id: false } // <-- disable `_id`
);
const schema = new Schema({
  subdoc: nestedSchema,
  docArray: [nestedSchema]
});
const Test = mongoose.model('Test', schema);

// Neither `subdoc` nor `docArray.0` will have an `_id`
await Test.create({
  subdoc: { name: 'test 1' },
  docArray: [{ name: 'test 2' }]
});
```

### Instance methods

Instances of `Models` are `documents`. Documents have many of their own [built-in instance methods](https://mongoosejs.com/docs/api/document.html). We may also define our own custom document instance methods

```JavaScript
// define a schema
const animalSchema = new Schema({ name: String, type: String },
  {
  // Assign a function to the "methods" object of our animalSchema through
		// schema options.

  // By following this approach, there is no need to create a separate TS 
		// type to define the type of the instance functions.
    methods: {
      findSimilarTypes(callback) {
        return mongoose.model('Animal').find({ type: this.type }, callback);
      }
    }
  });

// Or, assign a function to the "methods" object of our animalSchema
animalSchema.methods.findSimilarTypes = function(callback) {
  return mongoose.model('Animal').find({ type: this.type }, cb);
};
```

```JavaScript
const Animal = mongoose.model('Animal', animalSchema);
const dog = new Animal({ type: 'dog' });

dog.findSimilarTypes((err, dogs) => {
  console.log(dogs); // woof
});
```

### Statics

We can also add static functions to your model

```JavaScript
const animalSchema = new Schema({ name: String, type: String },
  {
  // Assign a function to the "statics" object of our animalSchema
		// through schema options.

  // By following this approach, there is no need to create a separate
		// TS type to define the type of the statics functions.
    statics: {
      findByName(name) {
        return this.find({ name: new RegExp(name, 'i') });
      }
    }
  });

// Or, Assign a function to the "statics" object of our animalSchema
animalSchema.statics.findByName = function(name) {
  return this.find({ name: new RegExp(name, 'i') });
};

// Or, equivalently, you can call `animalSchema.static()`.
animalSchema.static('findByBreed', function(breed) { 
		return this.find({ breed });
 });

const Animal = mongoose.model('Animal', animalSchema);
let animals = await Animal.findByName('fido');
animals = animals.concat(await Animal.findByBreed('Poodle'));
```

## SchemaTypes

> [!info] Mongoose v8.2.0: SchemaTypes  
> SchemaTypes handle definition of path  
> [https://mongoosejs.com/docs/schematypes.html](https://mongoosejs.com/docs/schematypes.html)  

==SchemaTypes== handle definition of path [defaults](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-default), [validation](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-validate), [getters](https://mongoosejs.com/docs/schematypes.html#getters), [setters](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-set), [field selection defaults](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-select) for [queries](https://mongoosejs.com/docs/api/query.html), and other general characteristics for ==**Mongoose**== document properties.

```JavaScript
const schema = new Schema({ name: String });
schema.path('name') instanceof mongoose.SchemaType; // true
schema.path('name') instanceof mongoose.Schema.Types.String; // true
schema.path('name').instance; // 'String'
```

> [!important] A
> 
> ==SchemaType== is ==different== from a ==type==. In other words, `mongoose.ObjectId !== mongoose.Types.ObjectId`. A ==SchemaType== is just a ==configuration object== for ==**Mongoose**==.  
> An instance of the   
> `mongoose.ObjectId` ==**SchemaType**== ==doesn't== actually create ==**MongoDB**== ==**ObjectIds**==, it is just a configuration for a path in a schema

### SchemaType Options

```JavaScript
const schema2 = new Schema({
  test: {
    type: String,
    lowercase: true // Always convert `test` to lowercase
  }
});

const numberSchema = new Schema({
  integerOnly: {
    type: Number,
    get: v => Math.round(v),
    set: v => Math.round(v),
    alias: 'i'
  }
});
```

### **All Schema Types**

- `required`
- `defaul`
- `select`: boolean, specifies default [projections](https://www.mongodb.com/docs/manual/tutorial/project-fields-from-query-results/) for queries
- `validate`: function, adds a [validator function](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
- `get`: function, defines a custom ==getter== for this property using [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).
- `set`: function, defines a custom ==setter== for this property using [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).
- `alias`: string, mongoose >= 4.10.0 only. Defines a [virtual](https://mongoosejs.com/docs/guide.html#virtuals) with the given name that gets/sets this path.
- `immutable`: boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has `isNew: true`.
- `transform`: function, Mongoose calls this function when you call [`Document#toJSON()`](https://mongoosejs.com/docs/api/document.html#document_Document-toJSON) function, including when you [`JSON.stringify()`](https://thecodebarbarian.com/the-80-20-guide-to-json-stringify-in-javascript) a document.

### Indexes

We can also define **[MongoDB indexes](https://www.mongodb.com/docs/manual/indexes/)** using schema type options.

- `index`: boolean, whether to define an [index](https://www.mongodb.com/docs/manual/indexes/) on this property.
- `unique`: boolean, whether to define a [unique index](https://www.mongodb.com/docs/manual/core/index-unique/) on this property.
- `sparse`: boolean, whether to define a [sparse index](https://www.mongodb.com/docs/manual/core/index-sparse/) on this property

### String

- `lowercase`: boolean, whether to always call `.toLowerCase()` on the value
- `uppercase`: boolean, whether to always call `.toUpperCase()` on the value
- `trim`: boolean, whether to always call [`.trim()`](https://masteringjs.io/tutorials/fundamentals/trim-string) on the value
- `match`: RegExp, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value matches the given regular expression
- `enum`: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is in the given array.
- `minLength`: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not less than the given number
- `maxLength`: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not greater than the given number
- `populate`: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

### Number

- `min`: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
- `max`: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
- `enum`: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is strictly equal to one of the values in the given array.
- `populate`: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

### Date

- `min`: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
- `max`: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
- `expires`: Number or String, creates a TTL index with the value expressed in seconds.

### ObjectId

- `populate`: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

  

## Models

==**Models**== are fancy constructors compiled from `Schema` definitions. An ==instance of a model== is called a `document`.

==Models== are responsible for creating and reading `documents` from the underlying ==**MongoDB database**==.

> [!info] Mongoose v8.2.0: Model  
> A Model is a class that's your primary tool for interacting with MongoDB.  
> [https://mongoosejs.com/docs/api/model.html](https://mongoosejs.com/docs/api/model.html)  

```JavaScript
const schema = new mongoose.Schema({ name: String, size: String });
const Tank = mongoose.model('Tank', schema);
```

### **Constructing Documents**

```JavaScript
const Tank = mongoose.model('Tank', yourSchema);

const small = new Tank({ size: 'small' });
await small.save();

// or

await Tank.create({ size: 'small' });

// or, for inserting large batches of documents
await Tank.insertMany([{ size: 'small' }]);
```

### **Querying**

Finding documents is easy with ==**Mongoose**==, which supports the rich query syntax of ==**MongoDB**==

```JavaScript
await Tank.find({ size: 'small' }).where('createdDate').gt(oneYearAgo).exec();
```

### Change Streams

==Change streams== provide a way for us to ==listen== to all inserts and updates going through your ==**MongoDB database**==

> [!info] Mongoose v8.2.0: MongoDB Change Streams in NodeJS with Mongoose  
> Change streams let you listen for updates to documents in a given model's collection, or even documents in an entire database.  
> [https://mongoosejs.com/docs/change-streams.html](https://mongoosejs.com/docs/change-streams.html)  

```JavaScript
async function run() {
  // Create a new mongoose model
  const personSchema = new mongoose.Schema({
    name: String
  });
  const Person = mongoose.model('Person', personSchema);

  // Create a change stream. The 'change' event gets emitted when there's a
  // change in the database
  Person.watch().
    on('change', data => console.log(new Date(), data));

  // Insert a doc, will trigger the change stream handler above
  console.log(new Date(), 'Inserting doc');
  await Person.create({ name: 'Axl Rose' });
}
```

  

## Documents

==**Mongoose**== `documents` represent a one-to-one mapping to `documents` as stored in ==**MongoDB**==.

Each `document` is an instance of its **Model**.

### Documents vs Models

==**Document**== and ==**Model**== are distinct classes in **Mongoose**. The ==**Model**== ==class== is a subclass of the ==**Document**== ==class==. When we use the ==Model constructor==, we create a new `document`

```JavaScript
const MyModel = mongoose.model('Test', new Schema({ name: String }));
const doc = new MyModel();

doc instanceof MyModel; // true
doc instanceof mongoose.Model; // true
doc instanceof mongoose.Document; // true
```

> [!important] We should not have to create an instance of the
> 
> `document` class without going through a `model`

### Validating

Documents are casted and validated before they are saved. ==**Mongoose**== first casts values to the ==specified== ==type== and then ==validates== them. Internally, ==**Mongoose**== calls the document's [`validate()`](https://mongoosejs.com/docs/api/document.html#document_Document-validate) method before ==saving==.

```JavaScript
const schema = new Schema({ name: String, age: { type: Number, min: 0 } });
const Person = mongoose.model('Person', schema);

const p = new Person({ name: 'foo', age: 'bar' });
// Cast to Number failed for value "bar" at path "age"
await p.validate();

const p2 = new Person({ name: 'foo', age: -1 });
// Path `age` (-1) is less than minimum allowed value (0).
await p2.validate();
```

  

## Subdocuments

==Subdocuments== are documents ==embedded== in other documents. In **Mongoose**, this means we can ==nest schemas in other schemas==

```JavaScript
const childSchema = new Schema({ name: 'string' });

const parentSchema = new Schema({
  // Array of subdocuments
  children: [childSchema],
  // Single nested subdocuments
  child: childSchema
})
```

==Subdocuments== are similar to normal documents. ==Nested schemas== can have [middleware](https://mongoosejs.com/docs/middleware.html), [custom validation logic](https://mongoosejs.com/docs/validation.html), virtuals, and any other feature top-level schemas can use. The ==major difference== is that ==subdocuments== are **==not saved individually==**, they are saved whenever their top-level ==parent document is saved==

```JavaScript
const Parent = mongoose.model('Parent', parentSchema);
const parent = new Parent({ children: [{ name: 'Matt' }, { name: 'Sarah' }] });
parent.children[0].name = 'Matthew';

// `parent.children[0].save()` is a no-op, it triggers middleware but
// does **not** actually save the subdocument. You need to save the parent
// doc.
await parent.save();
```

### **Subdocuments vs Nested Paths**

```JavaScript
// Subdocument
const subdocumentSchema = new mongoose.Schema({
  child: new mongoose.Schema({ name: String, age: Number })
});
const Subdoc = mongoose.model('Subdoc', subdocumentSchema);

// Nested path
const nestedSchema = new mongoose.Schema({
  child: { name: String, age: Number }
});
const Nested = mongoose.model('Nested', nestedSchema);
```

These two schemas look similar, and the `documents` in **MongoDB** will have the ==same structure== with both schemas. But there are a few Mongoose-specific ==differences==:

- Instances of `Nested` never have `child === undefined` . But instances of `Subdoc` can have `child === undefined`

### Find a `subdocument`

Each `subdocument` has an `_id` by default

==**Mongoose**== document arrays have a special [id()](https://mongoosejs.com/docs/api/mongoosedocumentarray.html#mongoosedocumentarray_MongooseDocumentArray-id) method for searching a document array to find a document with a given `_id`

```JavaScript
const doc = parent.children.id(_id);
```

### **Adding Subdocs to Arrays**

MongooseArray methods such as `push`, `unshift`, `addToSet`, and others cast arguments to their proper types transparently

```JavaScript
const Parent = mongoose.model('Parent');
const parent = new Parent();

// create a comment
parent.children.push({ name: 'Liesl' });
const subdoc = parent.children[0];
console.log(subdoc); // { _id: '501d86090d371bab2c0341c5', name: 'Liesl' }
subdoc.isNew; // true

await parent.save();
console.log('Success!');
```

We can also create a `subdocument` without adding it to an array by using the `create()` method of Document Arrays

```JavaScript
const newdoc = parent.children.create({ name: 'Aaron' });
```

### **Removing Subdocs**

```JavaScript
// Equivalent to `parent.children.pull(_id)`
parent.children.id(_id).deleteOne();

// Equivalent to `parent.child = null`
parent.child.deleteOne();

await parent.save();
console.log('the subdocs were removed');
```

### **Parents of Subdocs**

We can access the parent using the `parent()` function

```JavaScript
const schema = new Schema({
  docArr: [{ name: String }],
  singleNested: new Schema({ name: String })
});
const Model = mongoose.model('Test', schema);

const doc = new Model({
  docArr: [{ name: 'foo' }],
  singleNested: { name: 'bar' }
});

doc.singleNested.parent() === doc; // true
doc.docArr[0].parent() === doc; // true
```

If we have a ==deeply nested== `subdoc`, we can access the top-level document using the `ownerDocument()` function

```JavaScript
const schema = new Schema({
  level1: new Schema({
    level2: new Schema({
      test: String
    })
  })
});
const Model = mongoose.model('Test', schema);

const doc = new Model({ level1: { level2: 'test' } });

doc.level1.level2.parent() === doc; // false
doc.level1.level2.parent() === doc.level1; // true
doc.level1.level2.ownerDocument() === doc; // true
```

## Queries

==**Mongoose**== models provide several static helper functions for ==**CRUD operations**==

- `Model.deleteMany()`
- `Model.deleteOne()`
- `Model.find()`
- `Model.findById()`
- `Model.findByIdAndDelete()`
- `Model.findByIdAndRemove()`
- `Model.findByIdAndUpdate()`
- `Model.findOne()`
- `Model.findOneAndDelete()`
- `Model.findOneAndReplace()`
- `Model.findOneAndUpdate()`
- `Model.replaceOne()`
- `Model.updateMany()`
- `Model.updateOne()`

A ==mongoose query== can be executed in one of two ways

1. If we pass in a `callback` function, Mongoose will execute the query asynchronously and pass the results to the `callback`.
2. A query also has a `.then()` function, and thus can be used as a promise

### Executing

When executing a query, we specify your query as a ==JSON document==. The JSON document's syntax is the same as the **MongoDB shell**.

```JavaScript
// With a JSON doc
await Person.
  find({
    occupation: /host/,
    'name.last': 'Ghost',
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ['vaporizing', 'talking'] }
  }).
  limit(10).
  sort({ occupation: -1 }).
  select({ name: 1, occupation: 1 }).
  exec();

// Using query builder
await Person.
  find({ occupation: /host/ }).
  where('name.last').equals('Ghost').
  where('age').gt(17).lt(66).
  where('likes').in(['vaporizing', 'talking']).
  limit(10).
  sort('-occupation').
  select('name occupation').
  exec();
```

### Queries are not Promises

Mongoose queries are **not** promises. Queries are thenables, meaning they have a `.then()` method for `async/await` as a convenience. However, unlike promises, calling a query's `.then()` executes the query, so calling `then()` multiple times will throw an ==error==

```JavaScript
const q = MyModel.updateMany({}, { isDeleted: true });

await q.then(() => console.log('Update 2'));

// Throws "Query was already executed: Test.updateMany({}, { isDeleted: true })"
await q.then(() => console.log('Update 3'));
```

### Streaming

We can ==stream query results== from **MongoDB**. We need to call the `Query#cursor()` function to return an instance of **QueryCursor**.

```JavaScript
const cursor = Person.find({ occupation: /host/ }).cursor();

for (let doc = await cursor.next(); doc != null; doc = await cursor.next()) {
  console.log(doc); // Prints documents one at a time
}
```

### Aggregation

==Aggregation== can do many of the same things that queries can

> [!info] Mongoose v8.2.1: Aggregate  
> Aggregate constructor used for building aggregation pipelines.  
> [https://mongoosejs.com/docs/api/aggregate.html#aggregate_Aggregate](https://mongoosejs.com/docs/api/aggregate.html#aggregate_Aggregate)  

```JavaScript
const docs = await Person.aggregate([{ $match: { 'name.last': 'Ghost' } }]);
```

> [!important] However, just because we can use 
> 
> `aggregate()` doesn't mean we should. In general, we should use ==queries== where possible, and only use `aggregate()` when you absolutely need to.

  

Unlike query results, Mongoose does **not** [`hydrate()`](https://mongoosejs.com/docs/api/model.html#model_Model-hydrate) aggregation results. Aggregation results are always **POJOs**, not ==Mongoose documents==

```JavaScript
const docs = await Person.aggregate([{ $match: { 'name.last': 'Ghost' } }]);

docs[0] instanceof mongoose.Document; // false
```

  

Also, unlike query filters, **Mongoose** also doesn't  aggregation pipelines. That means we’re responsible for ensuring the values we pass in to an aggregation pipeline have the correct type

```JavaScript
const doc = await Person.findOne();

const idString = doc._id.toString();

// Finds the `Person`, because Mongoose casts `idString` to an ObjectId
const queryRes = await Person.findOne({ _id: idString });

// Does **not** find the `Person`, because Mongoose doesn't cast aggregation pipelines.
const aggRes = await Person.aggregate([{ $match: { _id: idString } }]);
```

### Query Casting

```JavaScript
const query = Character.find({ name: 'Jean-Luc Picard' });
query.getFilter(); // `{ name: 'Jean-Luc Picard' }`

// Subsequent chained calls merge new properties into the filter
query.find({ age: { $gt: 50 } });
query.getFilter(); // `{ name: 'Jean-Luc Picard', age: { $gt: 50 } }`
```

When we execute the query using `Query#exec()` or `Query#then()`, **Mongoose** casts the filter to match our ==schema==.

```JavaScript
// Note that `_id` and `age` are strings. Mongoose will cast `_id` to a MongoDB ObjectId and `age.$gt` to a number.
const query = Character.findOne({
  _id: '5cdc267dd56b5662b7b7cc0c',
  age: { $gt: '50' }
});

// `{ _id: '5cdc267dd56b5662b7b7cc0c', age: { $gt: '50' } }`
// Query hasn't been executed yet, so Mongoose hasn't casted the filter.
query.getFilter();

const doc = await query.exec();
doc.name; // "Jean-Luc Picard"

// Mongoose casted the filter, so `_id` became an ObjectId and `age.$gt` became a number.
query.getFilter()._id instanceof mongoose.Types.ObjectId; // true
typeof query.getFilter().age.$gt === 'number'; // true
```

> [!important] If
> 
> **Mongoose** fails to cast the filter to our ==schema==, our query will throw a `CastError`

### **The** `**strictQuery**` **Option**

By default, **Mongoose** does ==**not**== cast filter properties that aren't in your ==schema==

```JavaScript
const query = Character.findOne({ notInSchema: { $lt: 'not a number' } });

// No error because `notInSchema` is not defined in the schema
await query.exec();
```

We can configure this behavior using the `strictQuery` ==option for schemas==

```JavaScript
mongoose.deleteModel('Character');
const schema = new mongoose.Schema({ name: String, age: Number }, {
  strictQuery: true
});
Character = mongoose.model('Character', schema);

const query = Character.findOne({ notInSchema: { $lt: 'not a number' } });

await query.exec();
query.getFilter(); // Empty object `{}`, Mongoose removes `notInSchema`
```

  

To make Mongoose throw an error if our `filter` has a property that isn't in the schema, set `strictQuery` to `'throw'`

```JavaScript
mongoose.deleteModel('Character');
const schema = new mongoose.Schema({ name: String, age: Number }, {
  strictQuery: 'throw'
});
Character = mongoose.model('Character', schema);

const query = Character.findOne({ notInSchema: { $lt: 'not a number' } });

const err = await query.exec().then(() => null, err => err);
err.name; // 'StrictModeError'
// Path "notInSchema" is not in schema and strictQuery is 'throw'.
err.message;
```

### **Implicit** `**$in**`

Because of schemas, **Mongoose** knows what types fields should be, so it can provide some neat syntactic sugar

```JavaScript
// Normally wouldn't find anything because `name` is a string, but Mongoose automatically inserts `$in`
const query = Character.findOne({ name: ['Jean-Luc Picard', 'Will Riker'] });

const doc = await query.exec();
doc.name; // "Jean-Luc Picard"

// `{ name: { $in: ['Jean-Luc Picard', 'Will Riker'] } }`
query.getFilter();
```

### **How to Use** `**findOneAndUpdate()**` **in Mongoose**

> [!info] Mongoose v8.2.1: Mongoose Tutorials: How to Use `findOneAndUpdate()` in Mongoose  
> The findOneAndUpdate() function in Mongoose has a wide variety of use cases.  
> [https://mongoosejs.com/docs/tutorials/findoneandupdate.html](https://mongoosejs.com/docs/tutorials/findoneandupdate.html)  

Set the `new` option to `true` to return the document **after** `update` was applied

```JavaScript
const filter = { name: 'Jean-Luc Picard' };
const update = { age: 59 };

// `doc` is the document _after_ `update` was applied because of
// `new: true`
const doc = await Character.findOneAndUpdate(filter, update, {
  new: true
});
doc.name; // 'Jean-Luc Picard'
doc.age; // 59
```

  

> [!important] **Mongoose's**
> 
> `findOneAndUpdate()` is slightly different from the MongoDB Node.js driver's `findOneAndUpdate()` because it returns the ==document itself==, not a result ==object==.

  

Using the `upsert` option, you can use `findOneAndUpdate()` as a ==find-and-upsert== operation

```JavaScript
const filter = { name: 'Will Riker' };
const update = { age: 29 };

await Character.countDocuments(filter); // 0

const doc = await Character.findOneAndUpdate(filter, update, {
  new: true,
  upsert: true // Make this update into an upsert
});
doc.name; // Will Riker
doc.age; // 29
```

  

Set the `includeResultMetadata` flag to make **Mongoose** return the ==raw result== from **MongoDB**.

```JavaScript
const filter = { name: 'Will Riker' };
const update = { age: 29 };

await Character.countDocuments(filter); // 0

const res = await Character.findOneAndUpdate(filter, update, {
  new: true,
  upsert: true,
  // Return additional properties about the operation, not just the document
  includeResultMetadata: true
});

res.value instanceof Character; // true
// The below property will be `false` if MongoDB upserted a new document, and `true` if MongoDB updated an existing object.
res.lastErrorObject.updatedExisting; // false
```

### **Faster Mongoose Queries With Lean**

By default, **Mongoose** queries return an instance of the ==Mongoose Document class==. `Documents` are much heavier than vanilla **JavaScript objects**, because they have a lot of internal state for change tracking. Enabling the `lean` option tells **Mongoose** to skip ==instantiating a full Mongoose document== and just give you the **POJO**

```JavaScript
const schema = new mongoose.Schema({ name: String });
const MyModel = mongoose.model('Test', schema);

await MyModel.create({ name: 'test' });

const normalDoc = await MyModel.findOne();
// To enable the `lean` option for a query, use the `lean()` function.
const leanDoc = await MyModel.findOne().lean();

v8Serialize(normalDoc).length; // approximately 180
v8Serialize(leanDoc).length; // approximately 55, about 3x smaller!

// In case you were wondering, the JSON form of a Mongoose doc is the same as the POJO. 
// This additional memory only affects how much memory your Node.js process uses, not how much data is sent over the network.
JSON.stringify(normalDoc).length === JSON.stringify(leanDoc).length; // true
```

> [!important] Under the hood, after executing a query,
> 
> **Mongoose** ==converts== the query results from ==**POJOs**== to ==**Mongoose documents**==

  

The downside of enabling `lean` is that lean docs don't have:

- Change tracking
- Casting and validation
- Getters and setters
- Virtuals
- `save()`

```JavaScript
const personSchema = new mongoose.Schema({
  firstName: {
    type: String,
    get: capitalizeFirstLetter
  },
  lastName: {
    type: String,
    get: capitalizeFirstLetter
  }
});

personSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

function capitalizeFirstLetter(v) {
  // Convert 'bob' -> 'Bob'
  return v.charAt(0).toUpperCase() + v.substring(1);
}
const Person = mongoose.model('Person', personSchema);


// Create a doc and load it as a lean doc
await Person.create({ firstName: 'benjamin', lastName: 'sisko' });
const normalDoc = await Person.findOne();
const leanDoc = await Person.findOne().lean();

normalDoc.fullName; // 'Benjamin Sisko'
normalDoc.firstName; // 'Benjamin', because of `capitalizeFirstLetter()`
normalDoc.lastName; // 'Sisko', because of `capitalizeFirstLetter()`

leanDoc.fullName; // undefined
leanDoc.firstName; // 'benjamin', custom getter doesn't run
leanDoc.lastName; // 'sisko', custom getter doesn't run
```

  

> [!important] **When to Use Lean**
> 
>   
>   
> If we’re executing a query and sending the results without modification to, say, an [Express response](http://expressjs.com/en/4x/api.html#res), we should use `lean`

  

## Validation

- Validation is defined in the 
- Validation is  . **Mongoose** registers validation as a `pre('save')` ==hook on every schema== by default.
- Validation always runs as the **first** `pre('save')` hook. This means that validation ==doesn't run on any changes== we make in `pre('save')` hooks.
- We can disable automatic validation before save by setting the `[validateBeforeSave](https://mongoosejs.com/docs/guide.html#validateBeforeSave)` option
- We can manually run validation using `doc.validate()` or `doc.validateSync()`
- We can manually mark a field as invalid (causing validation to fail) by using [`doc.invalidate(...)`](https://mongoosejs.com/docs/api/document.html#document_Document-invalidate)
- Validators are ==not run on undefined values==. The only exception is the [`required`](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-required) validator.
- When we call `[Model#save](https://mongoosejs.com/docs/api/model.html#model_Model-save)`, **Mongoose** also runs ==subdocument validation==. If an error occurs, our `[Model#save](https://mongoosejs.com/docs/api/model.html#model_Model-save)` promise rejects
- Validation is customizable

  

> [!important] The 
> 
> `unique` Option is ==Not== a Validator

```JavaScript
const uniqueUsernameSchema = new Schema({
  username: {
    type: String,
    unique: true
  }
});
const U1 = db.model('U1', uniqueUsernameSchema);
const U2 = db.model('U2', uniqueUsernameSchema);

const dup = [{ username: 'Val' }, { username: 'Val' }];
// Race condition! This may save successfully, depending on whether MongoDB built the index before writing the 2 docs.
U1.create(dup).
  then(() => {
  }).
  catch(err => {
  });

// You need to wait for Mongoose to finish building the `unique` index before writing.
// You only need to build indexes once for a given collection, so you normally don't need to do this in production.
// But, if you drop the database between tests, you will need to use `init()` to wait for the index build to finish.
U2.init().
  then(() => U2.create(dup)).
  catch(error => {
    // `U2.create()` will error, but will *not* be a mongoose validation error, it will be a duplicate key error.
    // See: https://masteringjs.io/tutorials/mongoose/e11000-duplicate-key
    assert.ok(error);
    assert.ok(!error.errors);
    assert.ok(error.message.indexOf('duplicate key error') !== -1);
  })
```

### **Custom Validators**

If the ==built-in validators== aren't enough, we can define ==custom validators== to suit our ==needs==

```JavaScript
const userSchema = new Schema({
  phone: {
    type: String,
    validate: {
      validator: function(v) {
        return /\d{3}-\d{3}-\d{4}/.test(v);
      },
      message: props => `${props.value} is not a valid phone number!`
    },
    required: [true, 'User phone number required']
  }
});
```

### **Update Validators Only Run For Some Operations**

One final detail worth noting: update validators ==**only**== run on the following update operators:

- `$set`
- `$unset`
- `$push`
- `$addToSet`
- `$pull`
- `$pullAll`

## Middlewares

**Middleware** (also called ==pre== and ==post== ==_hooks_==) are functions which are passed control ==during execution== of asynchronous functions. **Middleware** is specified on the schema level and is useful for writing [plugins](https://mongoosejs.com/docs/plugins.html).

> [!info] Mongoose v8.2.0: Middleware  
> Middleware (also called pre and post hooks) are functions which are passed  
> [https://mongoosejs.com/docs/middleware.html](https://mongoosejs.com/docs/middleware.html)  

### **Types of Middleware**

Mongoose has 4 types of middleware:

- Document middleware
- Model middleware
- Aggregate middleware
- Query middleware

## Populate

**MongoDB** has the join-like [$lookup](https://www.mongodb.com/docs/manual/reference/operator/aggregation/lookup/) aggregation operator in versions >= 3.2. **Mongoose** has a more powerful alternative called `populate()`, which lets you reference documents in other collections.

==Population== is the process of automatically ==replacing== the specified ==paths== in the document with ==document(s) from other collection(s)==

> [!info] Mongoose v8.2.0: Query Population  
> MongoDB has the join-like $lookup aggregation operator in versions >= 3.  
> [https://mongoosejs.com/docs/populate.html](https://mongoosejs.com/docs/populate.html)  

```JavaScript
const mongoose = require('mongoose');
const { Schema } = mongoose;

const personSchema = Schema({
  _id: Schema.Types.ObjectId,
  name: String,
  age: Number,
  stories: [{ type: Schema.Types.ObjectId, ref: 'Story' }]
});

const storySchema = Schema({
  author: { type: Schema.Types.ObjectId, ref: 'Person' },
  title: String,
  fans: [{ type: Schema.Types.ObjectId, ref: 'Person' }]
});

const Story = mongoose.model('Story', storySchema);
const Person = mongoose.model('Person', personSchema);
```

### Saving refs

Saving refs to other documents works the same way we normally save properties, just assign the `_id` value:

```JavaScript
const author = new Person({
  _id: new mongoose.Types.ObjectId(),
  name: 'Ian Fleming',
  age: 50
});

await author.save();

const story1 = new Story({
  title: 'Casino Royale',
  author: author._id // assign the _id from the person
});

await story1.save();
// that's it!
```

### Population

```JavaScript
const story = await Story.
  findOne({ title: 'Casino Royale' }).
  populate('author').
  exec();

// prints "The author is Ian Fleming"
console.log('The author is %s', story.author.name);
```

Populated paths are no longer set to their original `_id` , their value is replaced with the ==mongoose document== returned from the database by performing a separate query before returning the results.

### Checking Whether a Field is Populated

```JavaScript
story.populated('author'); // truthy

story.depopulate('author'); // Make `author` not populated anymore
story.populated('author'); // undefined
```

  

> [!important] For convenience,
> 
> **Mongoose** adds a [`_id`](https://mongoosejs.com/docs/api/mongoose.html#mongoose_Mongoose-set) [getter to ObjectId instances](https://mongoosejs.com/docs/api/mongoose.html#mongoose_Mongoose-set) so we can use `story.author._id` regardless of whether `author` is populated.

```JavaScript
story.populated('author'); // truthy
story.author._id; // ObjectId

story.depopulate('author'); // Make `author` not populated anymore
story.populated('author'); // undefined

story.author instanceof ObjectId; // true
story.author._id; // ObjectId, because Mongoose adds a special getter
```

### Populate multiple paths

```JavaScript
await Story.
  find({ /* ... */ }).
  populate('fans').
  populate('author').
  exec();
```

But if we call `populate()` multiple times with the same path, only the last one will take effect

```JavaScript
// The 2nd `populate()` call below overwrites the first because they both populate 'fans'.
await Story.
  find().
  populate({ path: 'fans', select: 'name' }).
  populate({ path: 'fans', select: 'email' });
// The above is equivalent to:
await Story.find().populate({ path: 'fans', select: 'email' });
```

### Query conditions and other options

```JavaScript
await Story.
  find().
  populate({
    path: 'fans',
    match: { age: { $gte: 21 } },
    // Explicitly exclude `_id`
    select: 'name -_id'
  }).
  exec();
```

### `limit` vs `perDocumentLimit`

Populate does support a `limit` option, however, it currently does ==**not**== limit on a ==per-document basis== for backwards compatibility

```JavaScript
await Story.create([
  { title: 'Casino Royale', fans: [1, 2, 3, 4, 5, 6, 7, 8] },
  { title: 'Live and Let Die', fans: [9, 10] }
]);
```

If we were to `populate()` using the `limit` option.

```JavaScript
const stories = await Story.find().populate({
  path: 'fans',
  options: { limit: 2 }
});

stories[0].name; // 'Casino Royale'
stories[0].fans.length; // 2

// 2nd story has 0 fans!
stories[1].name; // 'Live and Let Die'
stories[1].fans.length; // 0
```

  

That's because, in order to avoid executing a separate query for each document, Mongoose instead queries for fans using `numDocuments * limit` as the limit. If you need the correct `limit`, you should use the `perDocumentLimit`

```JavaScript
const stories = await Story.find().populate({
  path: 'fans',
  // Special option that tells Mongoose to execute a separate query for each `story` to make sure we get 2 fans for each story.
  perDocumentLimit: 2
});

stories[0].name; // 'Casino Royale'
stories[0].fans.length; // 2

stories[1].name; // 'Live and Let Die'
stories[1].fans.length; // 2
```

> [!important] ==**Refs to children**==
> 
> > [!info] Mongoose v8.2.1: Query Population  
> > MongoDB has the join-like $lookup aggregation operator in versions >= 3.  
> > [https://mongoosejs.com/docs/populate.html#refs-to-children](https://mongoosejs.com/docs/populate.html#refs-to-children)  

## Discriminators

### The `model.discriminator()` function

==Discriminators== are a ==schema inheritance mechanism==. They enable us to have multiple models with overlapping ==schemas== on top of the same underlying **MongoDB collection**.

```JavaScript
const options = { discriminatorKey: 'kind' };

const eventSchema = new mongoose.Schema({ time: Date }, options);
const Event = mongoose.model('Event', eventSchema);

// ClickedLinkEvent is a special type of Event that has
// a URL.
const ClickedLinkEvent = Event.discriminator('ClickedLink',
  new mongoose.Schema({ url: String }, options));

// When you create a generic event, it can't have a URL field...
const genericEvent = new Event({ time: Date.now(), url: 'google.com' });
assert.ok(!genericEvent.url);

// But a ClickedLinkEvent can
const clickedEvent = new ClickedLinkEvent({ time: Date.now(), url: 'google.com' });
assert.ok(clickedEvent.url);
```

  

> [!important] **Discriminators**
> 
> save to the model's collection

```JavaScript
const event1 = new Event({ time: Date.now() });
const event2 = new ClickedLinkEvent({ time: Date.now(), url: 'google.com' });
const event3 = new SignedUpEvent({ time: Date.now(), user: 'testuser' });


await Promise.all([event1.save(), event2.save(), event3.save()]);
const count = await Event.countDocuments();
assert.equal(count, 3);
```

### Discriminator keys

The way **Mongoose** tells the ==difference== between the different discriminator models is by the '_discriminator key_', which is `__t` by default

```JavaScript
const event1 = new Event({ time: Date.now() });
const event2 = new ClickedLinkEvent({ time: Date.now(), url: 'google.com' });
const event3 = new SignedUpEvent({ time: Date.now(), user: 'testuser' });

assert.ok(!event1.__t);
assert.equal(event2.__t, 'ClickedLink');
assert.equal(event3.__t, 'SignedUp');
```

### **Embedded discriminators in arrays**

We can also define ==discriminators== on ==embedded document arrays==. Embedded discriminators are different because the ==different discriminator types== are stored in the ==same document array== (_within a document_) rather than the same collection

> [!info] Mongoose v8.2.1: Discriminators  
> Discriminators are a schema inheritance mechanism.  
> [https://mongoosejs.com/docs/discriminators.html#discriminators-save-to-the-event-models-collection](https://mongoosejs.com/docs/discriminators.html#discriminators-save-to-the-event-models-collection)  

## Plugins

==Schemas== are ==pluggable==, that is, they allow for applying pre-packaged capabilities to extend their functionality. This is a very powerful feature.

```JavaScript
// loadedAt.js
module.exports = function loadedAtPlugin(schema, options) {
  schema.virtual('loadedAt').
    get(function() { return this._loadedAt; }).
    set(function(v) { this._loadedAt = v; });

  schema.post(['find', 'findOne'], function(docs) {
    if (!Array.isArray(docs)) {
      docs = [docs];
    }
    const now = new Date();
    for (const doc of docs) {
      doc.loadedAt = now;
    }
  });
};

// game-schema.js
const loadedAtPlugin = require('./loadedAt');
const gameSchema = new Schema({ /* ... */ });
gameSchema.plugin(loadedAtPlugin);

// player-schema.js
const loadedAtPlugin = require('./loadedAt');
const playerSchema = new Schema({ /* ... */ });
playerSchema.plugin(loadedAtPlugin);
```

### Global plugins

Want to register a plugin for all schemas? The mongoose singleton has a `.plugin()` function that registers a plugin for every schema

```JavaScript
const mongoose = require('mongoose');
mongoose.plugin(require('./loadedAt'));

const gameSchema = new Schema({ /* ... */ });
const playerSchema = new Schema({ /* ... */ });

// `loadedAtPlugin` gets attached to both schemas
const Game = mongoose.model('Game', gameSchema);
const Player = mongoose.model('Player', playerSchema);
```

> [!important] Because many plugins rely on 
> 
> ==middleware==, we should make sure to apply plugins ==**before**== we call `mongoose.model()` or `conn.model()`

## Timestamps

**Mongoose schemas** support a `timestamps` option. If we set `timestamps: true`, **Mongoose** will add two properties of type `Date` to your schema:

1. `createdAt`: a date representing when this document was created (_immutable_)
2. `updatedAt`: a date representing when this document was last updated

```JavaScript
const userSchema = new Schema({ name: String }, { timestamps: true });
const User = mongoose.model('User', userSchema);

let doc = await User.create({ name: 'test' });

console.log(doc.createdAt); // 2022-02-26T16:37:48.244Z
console.log(doc.updatedAt); // 2022-02-26T16:37:48.244Z

doc.name = 'test2';
await doc.save();
console.log(doc.createdAt); // 2022-02-26T16:37:48.244Z
console.log(doc.updatedAt); // 2022-02-26T16:37:48.307Z

doc = await User.findOneAndUpdate({ _id: doc._id }, { name: 'test3' }, { new: true });
console.log(doc.createdAt); // 2022-02-26T16:37:48.244Z
console.log(doc.updatedAt); // 2022-02-26T16:37:48.366Z
```

### **Disabling Timestamps**

`save()`, `updateOne()`, `updateMany()`, `findOneAndUpdate()`, `update()`, `replaceOne()`, and `bulkWrite()` all support a `timestamps` option. Set `timestamps: false` to skip setting timestamps for that particular operation.

```JavaScript
let doc = await User.create({ name: 'test' });

console.log(doc.createdAt); // 2022-02-26T23:28:54.264Z
console.log(doc.updatedAt); // 2022-02-26T23:28:54.264Z

doc.name = 'test2';

// Setting `timestamps: false` tells Mongoose to skip updating `updatedAt` on this `save()`
await doc.save({ timestamps: false });
console.log(doc.updatedAt); // 2022-02-26T23:28:54.264Z

// Similarly, setting `timestamps: false` on a query tells Mongoose to skip updating `updatedAt`.
doc = await User.findOneAndUpdate({ _id: doc._id }, { name: 'test3' }, {
  new: true,
  timestamps: false
});
console.log(doc.updatedAt); // 2022-02-26T23:28:54.264Z
```

### Under the Hood

For queries with timestamps, **Mongoose** adds 2 properties to each update query:

1. Add `updatedAt` to `$set`
2. Add `createdAt` to `$setOnInsert`

If we run the code below:

```JavaScript
mongoose.set('debug', true);

const userSchema = new Schema({
  name: String
}, { timestamps: true });
const User = mongoose.model('User', userSchema);

await User.findOneAndUpdate({}, { name: 'test' });
```

We'll see the below output from Mongoose debug mode

```Bash
Mongoose: users.findOneAndUpdate({}, { '$setOnInsert': { createdAt: new Date("Sun, 27 Feb 2022 00:26:27 GMT") }, '$set': { updatedAt: new Date("Sun, 27 Feb 2022 00:26:27 GMT"), name: 'test' }}, {...})
```

**Notice** the `$setOnInsert` for `createdAt` and `$set` for `updatedAt`

MongoDB's [`$setOnInsert`](https://www.mongodb.com/docs/manual/reference/operator/update/setOnInsert/) operator applies the update only if a new document is ==upserted==. So, for example, if we want to _only_ set `updatedAt` if a new document is created, we can disable the `updatedAt` timestamp and set it as shown below:

```JavaScript
await User.findOneAndUpdate({}, { $setOnInsert: { updatedAt: new Date() } }, {
  timestamps: { createdAt: true, updatedAt: false }
});
```

  

## Transactions

==Transactions== let us execute ==multiple operations== in isolation and potentially ==undo all== the operations if ==one== of them ==fails==

 To create a transaction, we first need to create a session using `Mongoose#startSession` or `Connection#startSession()`

```JavaScript
// Using Mongoose's default connection
const session = await mongoose.startSession();

// Using custom connection
const db = await mongoose.createConnection(mongodbUri).asPromise();
const session = await db.startSession();
```

### The `session.withTransaction()` helper

- Creating a transaction
- Committing the transaction if it succeeds
- Aborting the transaction if your operation throws
- Retrying in the event of a ==[transient transaction error](https://stackoverflow.com/questions/52153538/what-is-a-transienttransactionerror-in-mongoose-or-mongodb)==.

```JavaScript
let session = null;

return Customer.createCollection().
  then(() => Customer.startSession()).
  // The `withTransaction()` function's first parameter is a function
  // that returns a promise.
  then( (_session) => {
	    session = _session;
	    return session.withTransaction(() => {
	      return Customer.create([{ name: 'Test' }], { session: session });
	    });
  }).
  then(() => Customer.countDocuments()).
  then(count => assert.strictEqual(count, 1)).
  then(() => session.endSession());
```

### With Mongoose Documents and `save()`

If we get a **Mongoose** document from `findOne()` or `find()` using a session, the document will keep a ==reference== to the session and use that session for `save()`

```JavaScript
const User = db.model('User', new Schema({ name: String }));

let session = null;

return User.createCollection().
  then(() => db.startSession()).
  then(_session => {
    session = _session;
    return User.create({ name: 'foo' });
  }).
  then(() => {
    session.startTransaction();
    return User.findOne({ name: 'foo' }).session(session);
  }).
  then(user => {
    // Getter/setter for the session associated with this document.
    assert.ok(user.$session());
    user.name = 'bar';
    // By default, `save()` uses the associated session
    return user.save();
  }).
  then(() => User.findOne({ name: 'bar' })).
  // Won't find the doc because `save()` is part of an uncommitted transaction
  then(doc => assert.ok(!doc)).
  then(() => session.commitTransaction()).
  then(() => session.endSession()).
  then(() => User.findOne({ name: 'bar' })).
	// Found here because it's saved
  then(doc => assert.ok(doc));
```

### With the Aggregation Framework

The `Model.aggregate()` function also supports ==transactions==. **Mongoose** aggregations have a `session()` helper that sets the session option.

```JavaScript
const Event = db.model('Event', new Schema({ createdAt: Date }), 'Event');

let session = null;

return Event.createCollection().
  then(() => db.startSession()).
  then(_session => {
    session = _session;
    session.startTransaction();
    return Event.insertMany([
      { createdAt: new Date('2018-06-01') },
      { createdAt: new Date('2018-06-02') },
      { createdAt: new Date('2017-06-01') },
      { createdAt: new Date('2017-05-31') }
    ], { session: session });
  }).
  then(() => Event.aggregate([
    {
      $group: {
        _id: {
          month: { $month: '$createdAt' },
          year: { $year: '$createdAt' }
        },
        count: { $sum: 1 }
      }
    },
    { $sort: { count: -1, '_id.year': -1, '_id.month': -1 } }
  ]).session(session)).
  then(res => assert.deepEqual(res, [
    { _id: { month: 6, year: 2018 }, count: 2 },
    { _id: { month: 6, year: 2017 }, count: 1 },
    { _id: { month: 5, year: 2017 }, count: 1 }
  ])).
  then(() => session.commitTransaction()).
  then(() => session.endSession());
```

### Advanced usage

```JavaScript
constCustomer = db.model('Customer',newSchema({ name:String }));

let session = null;
returnCustomer.createCollection().
then(() => db.startSession()).
then(_session => {
    session = _session;
// Start a transaction
    session.startTransaction();
// This `create()` is part of the transaction because of the `session` option.returnCustomer.create([{ name: 'Test' }], { session: session });
  }).
// Transactions execute in isolation, so unless you pass a `session` to `findOne()` you won't see the document until the transaction is committed.then(() =>Customer.findOne({ name: 'Test' })).
then(doc => assert.ok(!doc)).
// This `findOne()` will return the doc, because passing the `session` means this `findOne()` will run as part of the transaction.then(() =>Customer.findOne({ name: 'Test' }).session(session)).
then(doc => assert.ok(doc)).
// Once the transaction is committed, the write operation becomes visible outside of the transaction.then(() => session.commitTransaction()).
then(() =>Customer.findOne({ name: 'Test' })).
then(doc => assert.ok(doc)).
then(() => session.endSession());
```

  

We can also use `session.abortTransaction()` to abort a transaction

```JavaScript
let session = null;
returnCustomer.createCollection().
then(() =>Customer.startSession()).
then(_session => {
    session = _session;
    session.startTransaction();
returnCustomer.create([{ name: 'Test' }], { session: session });
  }).
then(() =>Customer.create([{ name: 'Test2' }], { session: session })).
then(() => session.abortTransaction()).
then(() =>Customer.countDocuments()).
then(count => assert.strictEqual(count, 0)).
then(() => session.endSession());
```

## TypeScripts supports

### Mongoose in TypeScript

1. Create an ==interface== representing a document in **MongoDB**
2. Create  corresponding to the document interface.
3. Create
4. **[Connect to MongoDB](https://mongoosejs.com/docs/connections.html)**

```TypeScript
import { Schema, model, connect } from 'mongoose';

// 1. Create an interface representing a document in MongoDB.
interface IUser {
  name: string;
  email: string;
  avatar?: string;
}

// 2. Create a Schema corresponding to the document interface.
const userSchema = new Schema<IUser>({
  name: { type: String, required: true },
  email: { type: String, required: true },
  avatar: String
});

// 3. Create a Model.
const User = model<IUser>('User', userSchema);

run().catch(err => console.log(err));

async function run() {
  // 4. Connect to MongoDB
  await connect('mongodb://127.0.0.1:27017/test');

  const user = new User({
    name: 'Bill',
    email: 'bill@initech.com',
    avatar: 'https://i.imgur.com/dM7Thhn.png'
  });
  await user.save();

  console.log(user.email); // 'bill@initech.com'
}
```

## ==API Reference==

> [!info] Mongoose v8.2.1: Mongoose  
> The exports object of the mongoose module is an instance of this class.  
> [https://mongoosejs.com/docs/api/mongoose.html](https://mongoosejs.com/docs/api/mongoose.html)