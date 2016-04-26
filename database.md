# Database class

## Table of Contents

* [Methods](#methods)
  * [connect([callback])](#connect)
  * [disconnect([callback])](#disconnect)
  * [schema(definition)](#schema)
  * [collection(name, [schema])](#collection)

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
