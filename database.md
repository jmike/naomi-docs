# Database

The Database class provides handy methods to connect/disconnect from a database, execute native queries and create schemas and collections. It maintains a collection pool internally to optimize performance and allow concurrent queries.

## Table of Contents

* [How to create a database](#how-to-create-a-database)
* [Methods](#methods)
  * [connect([callback])](#connect)
  * [disconnect([callback])](#disconnect)
  * [execute(query, [options], [callback])](#execute)
  * [query(query, [options], [callback])](#query)
  * [schema(definition)](#schema)
  * [collection(name, [schema])](#collection)

## How to create a database?

Creating a database instance is achieved through the [naomi#create()](naomi.md#create) method, e.g.

```javascript
var naomi = require('naomi');
var mysql = require('naomi-mysql');

naomi.register('mysql', mysql);

var db = naomi.create('mysql', {
  host: 'localhost',
  port: 3306,
  user: 'root',
  password: 'xxxxxxxx',
  database: 'my_schema'
});
```

## Methods

### <a name="connect" href="connect">#</a>connect([callback]) -> Promise

Connects to database using the connection properties specified at construction time.

##### Arguments

1. `callback` _(Function<Error>)_ callback function (optional).

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise.

##### Example

```javascript
db.connect()
  .then(() => {
    console.log('Connected to db');
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="disconnect" href="disconnect">#</a>disconnect([callback]) -> Promise

Disconnects from database.

##### Arguments

1. `callback` _(Function<Error>)_ callback function (optional).

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise.

##### Example

```javascript
db.disconnect()
  .then(() => {
    console.log('Disconnected from db');
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="execute" href="execute">#</a>execute(query, [options], [callback]) -> Promise

Executes the given native query and returns results.

##### Arguments

1. `query` _(Object)_ native query object (required).
2. `options` _(Object)_ query options (optional).
3. `callback` _(Function<Error, (Object, Array\<Object\>)>)_ callback function (optional).

###### MySQL-specific arguments

* `query.sql` _(string)_ a parameterized SQL statement (required).
* `query.params` _(Array)_ parameter values (optional, defaults to `[]`).

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to the query results.

##### MySQL Example

```javascript
db.run({
  sql: 'SELECT * FROM `employees` WHERE id = ? LIMIT 1;',
  params: [7]
})
  .then((results) => {
    // do something with results
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="query" href="query">#</a>query(query, [options], [callback]) -> Promise

Alias of [Database#run()](#run) for compatibility with earlier Naomi versions.

### <a name="schema" href="schema">#</a>schema(definition) -> [Schema](schema.md)

Constructs and returns a new Schema with the supplied keys definition.

##### Arguments

1. `definition` _(Object\<string, Object\>)_ key-value pairs where key is the name of a key and value its related properties

Bear in mind that `type` in the properties object references a datatype. The rest of the attributes will be directly assigned to the datatype. For further info please consult the [datatypes docs](datatypes.md).

##### Returns

Returns a new [Schema](schema.md) instance.

##### Example

```javascript
var employees = db.schema({
  id: { type: 'integer', autoinc: true },
  firstname: { type: 'string', maxLength: 45 },
  lastname: { type: 'string', maxLength: 45 },
  email: { type: 'email', trim: true },
  age: { type: 'string', min: 18, max: 100 }
});
```

### <a name="collection" href="collection">#</a>collection(name, [schema]) -> [Collection](collection.md)

Constructs and returns a new Collection with the specified schema.

##### Arguments

1. `name` _(string)_ the name of the collection.
2. `schema` _(Object, [Schema](schema.md))_ the collection schema (optional).

##### Returns

Returns a new [Collection](collection.md) instance.

##### Example

```javascript
var employees = db.collection('employees', {
  id: {type: 'integer', autoinc: true},
  firstname: {type: 'string', maxLength: 45},
  lastname: {type: 'string', maxLength: 45},
  email: {type: 'email', trim: true},
  age: {type: 'string', min: 18, max: 100}
});
```
