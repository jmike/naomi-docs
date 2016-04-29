# Query Language

The naomi mongo-like query language.

## Table of Contents

* [Selection](#selection)
  * [$eq](#eq)
  * [$ne](#ne)
  * [$lt](#lt)
  * [$lte](#lte)
  * [$gt](#gt)
  * [$gte](#gte)
  * [$in](#in)
  * [$nin](#nin)
  * [$like](#like)
  * [$nlike](#nlike)
  * [$id](#id)
  * [$and](#and)
  * [$or](#or)
* [Projection](#projection)
* [OrderBy](#orderby)
* [Limit](#limit)
* [Offset](#offset)

### <a name="selection" href="#selection">#</a>Selection

The selection expression specifies the records to return in a query operation.

##### Accepted Values

* _Object_ with operators (see [below](#and))
* Plain values, i.e. _boolean, number, string, Date, Buffer_
* _Array\<*\>_ an array containing any of the above

##### Notes

A selection expression normally accepts an _Object_ containing selection operators as described [below](#and).

Nevertheless, selection expressions may also specify plain values, e.g. 

```javascript
var selection = \<value\>; // i.e. boolean, number, string, Date, Buffer
```

The above would be interpreted as follows:

```javascript
{ $id: { $eq: \<value\> } }
```

Arrays are also accepted, e.g.

```javascript
var selection = [{ firstname: { $ne: 'Jack' } }, 10];
```

The above would be interpreted as follows:

```javascript
{
  $or: [
    { firstname: { $ne: 'Jack' } },
    { $id: { $eq: 10 } },
  ]
}
```

##### Example with plain value

```javascript
var selection = 14;
```

Given a collection with `id` primary key, the above would be the rough equivalent of:

```sql
id = 14
```

##### Example with array

```javascript
var selection = [1, 2, { firstname: { $eq: 'Jack' } }];
```

Given a collection with `id` primary key, the above would be the rough equivalent of:

```sql
id = 1 OR id = 2 OR firstname = 'Jack'
```

### <a name="eq" href="#eq">$</a>eq

"Equals with" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  id: {
    $eq: 1
  }
};
```

The above would be the rough equivalent of:

```sql
id = 1
```

The same can be simply written as:

```javascript
var selection = {
  id: 1 // $eq is implied
};
```

### <a name="ne" href="#ne">$</a>ne

"Not equal with" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $ne: 20
  }
};
```

The above would be the rough equivalent of:

```sql
age != 20
```

### <a name="lt" href="#lt">$</a>lt

"Less than" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $lt: 30
  }
};
```

The above would be the rough equivalent of:

```sql
age < 30
```

### <a name="lte" href="#lte">$</a>lte

"Less than or equal" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $lte: 30
  }
};
```

The above would be the rough equivalent of:

```sql
age <= 30
```

### <a name="gt" href="#gt">$</a>gt

"Greater than" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $gt: 18
  }
};
```

The above would be the rough equivalent of:

```sql
age > 18
```

### <a name="gte" href="#gte">$</a>gte

"Greater than or equal" operator.

##### Accepted Values

_string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $gte: 18
  }
};
```

The above would be the rough equivalent of:

```sql
age >= 30
```

### <a name="in" href="#in">$</a>in

"In" operator.

##### Accepted Values

_Array of string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $in: [18, 30]
  }
};
```

The above would be the rough equivalent of:

```sql
age IN (18, 30)
```

### <a name="nin" href="#nin">$</a>nin

"Not in" operator.

##### Accepted Values

_Array of string, number, boolean, Date, Buffer_

##### Example

```javascript
var selection = {
  age: {
    $nin: [19, 31]
  }
};
```

The above would be the rough equivalent of:

```sql
age NOT IN (19, 31)
```

### <a name="like" href="#like">$</a>like

"Like" operator.

##### Accepted Values

_string_

##### Example

```javascript
var selection = {
  firstname: {
    $like: 'Joh%'
  }
};
```

The above would be the rough equivalent of:

```sql
firstname LIKE 'Joh%'
```

### <a name="nlike" href="#nlike">$</a>nlike

"Not like" operator.

##### Accepted Values

_string_

##### Example

```javascript
var selection = {
  firstname: {
    $nlike: '%ar'
  }
};
```

The above would be the rough equivalent of:

```sql
firstname NOT LIKE '%ar'
```

### <a name="id" href="#id">$</a>id

Special ID clause; $id will be replaced with the primary key column.

##### Example

```javascript
var selection = {
  $id: {
    $ne: 15
  }
};
```

Given a table with an atomic primary key named "id", the above would be the rough equivalent of:

```sql
id != 15
```

### <a name="and" href="#and">$</a>and

"Logical and" operator.

##### Accepted Values

_Array_

##### Example

```javascript
var selection = {
  $and: [
    {firstname: 'john'}
    {lastname: 'doe'}
  ]
};
```

The above would be the rough equivalent of:

```sql
(firstname = 'john') AND (lastname = 'doe')
```

### <a name="or" href="#or">$</a>or

"Logical or" operator.

##### Accepted Values

_Array_

##### Example

```javascript
var selection = {
  $or: [
    {firstname: 'john'}
    {firstname: 'maria'}
  ]
};
```

The above would be the rough equivalent of:

```sql
(firstname = 'john') OR (firstname = 'maria')
```

### <a name="projection" href="#projection">#</a>Projection

The projection expression limits the keys returned from a query operation by specifying inclusion and exclusion of fields.

##### Accepted Values

_Object\<string, number\>_ where number is 1 or true for inclusion and -1 or false for exclusion

##### Example with inclusion

```javascript
var projection = {
  firstname: 1,
  lastname: 1
};
```

The above would be the rough equivalent of:

```sql
SELECT firstname, lastname
```

##### Example with exclusion

```javascript
var projection = {
  id: -1
};
```

Given a collection with `id`, `firstname`, `lastname` and `age` keys, the above would be the rough equivalent of:

```sql
SELECT firstname, lastname, age; // id is excluded
```
