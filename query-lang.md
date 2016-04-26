# Query Language

The naomi mongo-like query language.

## Table of Contents

* [$and](#and)
* [$or](#or)
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

### <a name="and" href="#and">$</a>and

"Logical and" expression.

##### Accepted Values

_Array_

##### Example

```javascript
var $query = {
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

"Logical or" expression.

##### Accepted Values

_Array_

##### Example

```javascript
var $query = {
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

### <a name="eq" href="#eq">$</a>eq

"Equals with" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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
var $query = {
  id: 1 // $eq is implied
};
```

### <a name="ne" href="#ne">$</a>ne

"Not equal with" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Less than" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Less than or equal" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Greater than" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Greater than or equal" expression.

##### Accepted Values

_String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"In" expression.

##### Accepted Values

_Array of String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Not in" expression.

##### Accepted Values

_Array of String, Number, Boolean, Date, Buffer_

##### Example

```javascript
var $query = {
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

"Like" expression.

##### Accepted Values

_String_

##### Example

```javascript
var $query = {
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

"Not like" expression.

##### Accepted Values

_String_

##### Example

```javascript
var $query = {
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
var $query = {
  $id: {
    $ne: 15
  }
};
```

Given a table with an atomic primary key named "id", the above would be the rough equivalent of:

```sql
id != 15
```
