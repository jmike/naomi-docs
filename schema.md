# Schema

The Schema class holds information on a collection's keys and indices. It can be used to validate records before inserting to a [collection](collection.md).

## Table of Contents

* [How to create a schema](#how-to-create-a-schema)
* [Methods](#methods)
  * [extend(spec)](#extend)
  * [index(payload, [options])](#index)
  * [hasKey(key)](#hasKey)
  * [getKeys()](#getKeys)
  * [getPrimaryKey()](#getPrimaryKey)
  * [getUniqueKey(name)](#getUniqueKey)
  * [getIndexKey(name)](#getIndexKey)
  * [isKeyAutoInc(key)](#isKeyAutoInc)
  * [isPrimaryKey(...keys)](#isPrimaryKey)
  * [isUniqueKey(...keys)](#isUniqueKey)
  * [isIndexKey(...keys)](#isIndexKey)
  * [hasAtomicPrimaryKey()](#hasAtomicPrimaryKey)
  * [hasAutoIncPrimaryKey()](#hasAutoIncPrimaryKey)
  * [validate(record, [keys], [callback])](#validate)
  * [toJoi()](#toJoi)
  * [toJSON()](#toJSON)

## How to create a schema?

Schema instances should always be created using the [Database#schema()](database.md#collection) method, e.g.

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

var schema = db.schema({
  id: { type: 'integer', autoinc: true, min: 0 },
  firstname: { type: 'string', maxLength: 45, nullable: true },
  lastname: { type: 'string', maxLength: 45, nullable: true },
  age: { type: 'integer', min: 18, max: 100 }
});
```

## Methods

### <a name="extend" href="extend">#</a>extend(spec) -> Schema

Extends schema with the given spec object.

##### Arguments

1. `spec` _(Object)_ where keys are the name

##### Returns

Returns _this_ Schema to allow method chaining.

##### Throws

_(TypeError)_ if spec is invalid.

##### Example

```javascript
schema.extend({
  age: {type: 'integer', min: 18, max: 99}, // overwrite previously-defined age with min and max properties
  date_employed: date: {type: 'date', min: '2016-03-25', format: 'YYYY-MM-DD'},
});
```

### <a name="index" href="index">#</a>index(payload, options) -> Schema

Creates the specified index in schema.

##### Arguments

1. `payload` _(Object)_ a plain object where keys are keys already defined in this schema and values represent the type of the index, i.e. 1 for ASC, -1 for DESC
2. `options` _(Object)_ index options (optional)
  * `name` _(string)_ the name of the index in schema (optional)
  * `type` _(string)_ the type of the index, i.e. "primary", "unique" or "index" (optional; defaults to "index")

##### Returns

Returns _this_ Schema to allow method chaining.

##### Throws

_(TypeError)_ if payload or options are invalid.

##### Example

```javascript
schema.index({
  age: -1
}, {
  name: 'idx_age',
  type: 'index'
});
```

### <a name="hasKey" href="hasKey">#</a>hasKey(key) -> boolean

Indicates whether the specified key exists in schema.

##### Arguments

1. `key` _(string)_ the name of the key

##### Returns

Returns true if key exists, false if not.

##### Example

```javascript
if (schema.hasKey('firstname')) {
  console.log('firstname exists in schema');
}
```

### <a name="getKeys" href="getKeys">#</a>getKeys() -> Array\<string\>

Returns an array of keys specified in this schema.

##### Example

```javascript
schema.getKeys().forEach((key) => {
  // do something with key
});
```

### <a name="getPrimaryKey" href="getPrimaryKey">#</a>getPrimaryKey() -> Array\<string\>

Returns an array of keys that compose the primary key index of this schema.

##### Example

```javascript
schema.getPrimaryKey().forEach((key) => {
  // do something with key
});
```

##### Note

Schema can only have 1 primary key index though it may be compound, i.e. composed of 1+ keys.

### <a name="getUniqueKey" href="getUniqueKey">#</a>getUniqueKey(name) -> Array\<string\>

Returns an array of keys that compose the designated unique key index of this schema.

##### Arguments

1. `name` _(string)_ the name of the unique key index

##### Example

```javascript
schema.getUniqueKey('uidx_name').forEach((key) => {
  // do something with key
});
```

##### Note

Schema can only have multiple unique key indices, hence the need to specify the index name.

### <a name="getIndexKey" href="getIndexKey">#</a>getIndexKey(name) -> Array\<string\>

Returns an array of keys that compose the designated _plain_ index of this schema.

##### Arguments

1. `name` _(string)_ the name of the plain index

##### Example

```javascript
schema.getIndexKey('idx_age').forEach((key) => {
  // do something with key
});
```

##### Note

Schema can only have multiple _plain_ indices, hence the need to specify the index name.

### <a name="isKeyAutoInc" href="isKeyAutoInc">#</a>isKeyAutoInc(key) -> boolean

Indicates whether the designated key is automatically incremented.

##### Arguments

1. `key` _(string)_ the name of the key

##### Example

```javascript
if (schema.isKeyAutoInc('id')) {
  console.log('id is autoinc');
}
```

### <a name="isPrimaryKey" href="isPrimaryKey">#</a>isPrimaryKey(...keys) -> boolean

Indicates whether the specified key(s) compose the primary key of this schema.

##### Arguments

1. `keys` _(...string)_ the names of the keys

##### Example

```javascript
if (schema.isPrimaryKey('id')) {
  console.log('id is PK');
}
```

##### Note

Primary keys may be compound, i.e. composed of multiple keys. Hence the use of [rest params](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/rest_parameters) in this function.

### <a name="isUniqueKey" href="isUniqueKey">#</a>isUniqueKey(...keys) -> boolean

Indicates whether the specified key(s) compose a unique key of this schema.

##### Arguments

1. `keys` _(...string)_ the names of the keys

##### Example

```javascript
if (schema.isUniqueKey('firstname', 'lastname')) {
  console.log('firstname and lastname compose a unique key');
}
```

##### Note

Unique keys may be compound, i.e. composed of multiple keys. Hence the use of [rest params](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/rest_parameters) in this function.

### <a name="isIndexKey" href="isIndexKey">#</a>isIndexKey(...keys) -> boolean

Indicates whether the specified key(s) compose an index key of this schema.

##### Arguments

1. `keys` _(...string)_ the names of the keys

##### Example

```javascript
if (schema.isIndexKey('age')) {
  console.log('age is index key');
}
```

##### Note

Index keys may be compound, i.e. composed of multiple keys. Hence the use of [rest params](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/rest_parameters) in this function.

### <a name="hasAtomicPrimaryKey" href="hasAtomicPrimaryKey">#</a>hasAtomicPrimaryKey() -> boolean

Indicates whether this schema has an atomic (i.e. consisted of a single key) primary key.

##### Example

```javascript
if (schema.hasAtomicPrimaryKey()) {
  console.log('schema has an atomic primary key');
}
```

### <a name="hasAutoIncPrimaryKey" href="hasAutoIncPrimaryKey">#</a>hasAutoIncPrimaryKey() -> boolean

Indicates whether this schema has an auto-incremented primary key.

##### Example

```javascript
if (schema.hasAutoIncPrimaryKey()) {
  console.log('primary key is auto-incremented');
}
```

### <a name="validate" href="validate">#</a>validate(record, keys, callback) -> Promise

Validates and returns the designated record.

##### Arguments

1. `record` _(Object)_ the record to validate
2. `keys` _(Array\<string\>)_ array of keys to include in validation (optional; default to all keys)
3. `callback` _(Function<Error, Object>)_ callback function (optional)

##### Example

```javascript
schema.validate({
  firstname: 'Donnie',
  lastname: 'Azoff',
  age: 36
})
  .then((record) => {
    // do something with validated record
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="toJoi" href="toJoi">#</a>toJoi() -> Joi

Returns a [Joi](https://github.com/hapijs/joi) validator based on this schema.

### <a name="toJSON" href="toJSON">#</a>toJSON() -> Object

Returns a JSON representation of the keys of this schema.

##### Note

Indices are not included in JSON object.
