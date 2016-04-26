# Collection

## Table of Contents

* [Methods](#methods)
  * [find([selector], [options], [callback])](#find)
  * [findOne([selector], [options], [callback])](#findOne)

## Methods

### <a name="find" href="find">#</a>find([selector], [options], [callback]) -> Promise

Retrieves the designated records from the collection.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (optional)
2. `options` _(Object)_ query options (optional)
  * `options.projection` _(Object)_ a naomi projection expression
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression
  * `options.limit` _(integer)_ maximum number of records to retrieve
  * `options.offset` _(integer)_ number of records to skip
3. `callback` _(Function\<Error, Array\<Object\>\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to an array of records.

##### Example

```javascript
db.find({ age: { $gte: 18 } })
  .then((records) => {
    // do something with records
  })
  .catch((err) => {
    console.error(err);
  });
```

##### Notes

Method will return an empty array if records are not found in the collection.

### <a name="findOne" href="findOne">#</a>findOne([selector], [options], [callback]) -> Promise

Retrieves a single designated record from the collection.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (optional)
2. `options` _(Object)_ query options (optional)
  * `options.projection` _(Object)_ a naomi projection expression
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression
  * `options.offset` _(integer)_ number of records to skip
3. `callback` _(Function\<Error, (Object, undefined)\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to a single record.

##### Example

```javascript
db.findOne({ id: 10 })
  .then((record) => {
    // do something with record
  })
  .catch((err) => {
    console.error(err);
  });
```

##### Notes

Method will return `undefined` if record is not found in the collection.
