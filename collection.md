# Collection

## Table of Contents

* [Methods](#methods)
  * [find([selector], [options], [callback])](#find)
  * [findOne([selector], [options], [callback])](#findOne)
  * [count([selector], [options], [callback])](#count)
  * [remove([selector], [options], [callback])](#remove)
  * [insert(records, [options], [callback])](#insert)
  * [upsert(records, [options], [callback])](#upsert)
  * [update(selector, payload, [options], [callback])](#update)

## Methods

### <a name="find" href="find">#</a>find([selector], [options], [callback]) -> Promise

Retrieves the designated records from the collection.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (optional)
2. `options` _(Object)_ query options (optional)
  * `options.projection` _(Object)_ a naomi projection expression (optional)
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression (optional)
  * `options.limit` _(number)_ maximum number of records to retrieve (optional)
  * `options.offset` _(number)_ number of records to skip (optional)
3. `callback` _(Function\<Error, Array\<Object\>\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to an array of records.

##### Example

```javascript
collection.find({ age: { $gte: 18 } })
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
  * `options.projection` _(Object)_ a naomi projection expression (optional)
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression (optional)
  * `options.offset` _(number)_ number of records to skip (optional)
3. `callback` _(Function\<Error, (Object, undefined)\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to a single record.

##### Example

```javascript
collection.findOne({ id: 10 })
  .then((record) => {
    // do something with record
  })
  .catch((err) => {
    console.error(err);
  });
```

##### Notes

Method will return `undefined` if record is not found in the collection.

### <a name="count" href="count">#</a>count([selector], [options], [callback]) -> Promise

Counts the designated records in the collection.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (optional)
2. `options` _(Object)_ query options (optional)
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression (optional)
  * `options.limit` _(number)_ maximum number of records to retrieve (optional)
  * `options.offset` _(number)_ number of records to skip (optional)
3. `callback` _(Function\<Error, number\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to the count of records.

##### Example

```javascript
collection.count({ age: { $gte: 18 } })
  .then((n) => {
    console.log(`Found ${n} record(s)`);
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="remove" href="remove">#</a>remove([selector], [options], [callback]) -> Promise

Removes the designated records from the collection.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (optional)
2. `options` _(Object)_ query options (optional)
  * `options.orderby` _(string, Object, Array\<string, Object\>)_ a naomi orderby expression (optional)
  * `options.limit` _(number)_ maximum number of records to retrieve (optional)
3. `callback` _(Function\<Error\>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise that will resolve when records have been successfully removed.

##### Example

```javascript
collection.remove({ age: { $lt: 18 } })
  .then(() => {
    console.log(`Removed all employees under the age of 18`);
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="insert" href="insert">#</a>insert(records, [options], [callback]) -> Promise

Inserts the supplied record(s) to the collection.

##### Arguments

1. `records` _(Object, Array\<Object\>)_ record(s) to insert to the collection (required)
2. `options` _(Object)_ query options (optional)
3. `callback` _(Function\<Error\, (Object, Array\<Object\>)>)_ callback function (optional)

###### MySQL-specific arguments

* `options.ignore` _(boolean)_ if true MySQL will perform an `INSERT IGNORE` query (optional, defaults to `false`)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to the primary key of the records inserted.

##### Example

```javascript
collection.insert([
  { firstname: 'Mr.', lastname: 'Doobs', age: 18 },
  { firstname: 'George', lastname: 'Fudge', age: 19 },
  { firstname: 'Jack', lastname: 'White', age: 20 }
 ])
  .then((pk) => {
    // do something with pk array
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="upsert" href="upsert">#</a>upsert(records, [options], [callback]) -> Promise

Upserts (i.e. updates or creates if records don't exist) the supplied record(s) to the collection.

##### Arguments

1. `records` _(Object, Array\<Object\>)_ record(s) to upsert to the collection (required)
2. `options` _(Object)_ query options (optional)
3. `callback` _(Function\<Error\, (Object, Array\<Object\>)>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise resolving to the primary key of the records upserted.

##### Example

```javascript
collection.upsert([
  { firstname: 'Mr.', lastname: 'Doobs', age: 19 }
 ])
  .then((pk) => {
    // do something with pk array
  })
  .catch((err) => {
    console.error(err);
  });
```

### <a name="update" href="update">#</a>update(selector, payload, [options], [callback]) -> Promise

Updates the designated record(s) in the collection with the supplied payload.

##### Arguments

1. `selector` _(boolean, number, string, Date, Object, Array\<Object\>)_ a naomi selection expression (required)
1. `payload` _(Object)_ key-value pairs to set in the designated records (required)
2. `options` _(Object)_ query options (optional)
3. `callback` _(Function\<Error\, (Object, Array\<Object\>)>)_ callback function (optional)

##### Returns

Returns a [bluebird](http://bluebirdjs.com/docs/api-reference.html) promise that will resolve when records have been successfully updated.

##### Example

```javascript
collection.update({ id: 2 }, { age: 20 })
  .then(() => {
    console.log(`Employee #2 has been successfully updated`);
  })
  .catch((err) => {
    console.error(err);
  });
```
