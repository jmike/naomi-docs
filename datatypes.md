# Datatypes

A detailed description of Naomi datatypes and their related properties.

## Table of Contents

* [binary](#binary)
  * [binary.default(value)](#binarydefault)
  * [binary.encoding(encoding)](#binaryencoding)
  * [binary.length(limit)](#binarylength)
  * [binary.maxLength(limit)](#binarymaxlength)
  * [binary.minLength(limit)](#binaryminlength)
  * [binary.nullable(nullable)](#binarynullable)
* [boolean](#boolean)
  * [boolean.nullable(nullable)](#booleannullable)
* [date](#date)
  * [date.default(value)](#datedefault)
  * [date.format(format)](#dateformat)
  * [date.max(value)](#datemax)
  * [date.min(value)](#datemin)
  * [date.nullable(nullable)](#datenullable)

## binary

The binary datatype matches [Buffer](https://nodejs.org/api/buffer.html) and string types (the latter being converted to Buffer internally).

### <a name="binarydefault" href="binarydefault">#</a>binary.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(buffer, Function)_ the default value

##### Example

```javascript
binary.default(new Buffer([0x62,0x75,0x66,0x66,0x65,0x72]));
```

##### Notes

You may also specify a function to return the default value.

### <a name="binaryencoding" href="binaryencoding">#</a>binary.encoding(encoding)

Sets character encoding for string inputs.

##### Parameters

1. `encoding` _(string)_ a character encoding - see [Node.js docs](https://nodejs.org/api/buffer.html#buffer_buffers_and_character_encodings) for further info

##### Example

```javascript
binary.encoding('base64');
```

### <a name="binarylength" href="binarylength">#</a>binary.length(limit)

Specifies the exact length of the buffer.

##### Parameters

1. `limit` _(number)_ the exact length required.

##### Example

```javascript
binary.length(3);
```

### <a name="binarymaxlength" href="binarymaxlength">#</a>binary.maxLength(limit)

Specifies the maximum length of the buffer.

##### Parameters

1. `limit` _(number)_ the maximum length allowed.

##### Example

```javascript
binary.maxLength(5);
```

### <a name="binaryminlength" href="binaryminlength">#</a>binary.minLength

Specifies the minimum length of the buffer.

##### Parameters

1. `minLength` _(number)_ the minimum length allowed.

##### Example

```javascript
binary.minLength(1);
```

### <a name="binarynullable" href="binarynullable">#</a>binary.nullable(nullable)

Marks the datatype as optional, which allows `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
binary.nullable(true); // allows nil values
```


## boolean

The boolean datatype matches boolean types (as well as the strings 'true', 'false', 'yes', 'no', 'on' or 'off').

### <a name="booleannullable" href="booleannullable">#</a>boolean.nullable(nullable)

Marks the datatype as optional, which allows `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
boolean.nullable(true); // allows nil values
```


## date

The date datatype matches Date types, JavaScript date string and number of milliseconds.

### <a name="datedefault" href="datedefault">#</a>date.default(value)

Sets a default value for this datatype.

##### Parameters

1. `default` _(string, Date, Function)_ the default value.

##### Example

```javascript
date.default('2016-02-29');
```

##### Notes

You may also specify a function to return the default value, e.g.

```javascript
date.default(Date.now);
```

### <a name="dateformat" href="dateformat">#</a>date.format(format)

Specifies the allowed date format.

##### Parameters

1. `format` _(string)_ a string that follows the moment.js [format](http://momentjs.com/docs/#/parsing/string-format/).

##### Example

```javascript
date.format('YYYY-MM-DD');
```

### <a name="datemax" href="datemax">#</a>date.max(value)

Specifies the latest date allowed.

##### Parameters

1. `value` _(string)_ string representation of the latest date allowed.

##### Example

```javascript
date.max('2016-03-25');
```

##### Notes

You may use `now` instead of an actual date so as to always compare relatively to the current date, allowing to explicitly ensure a date is either in the past or in the future, e.g.

```javascript
date.max('now');
```

### <a name="datemin" href="datemin">#</a>date.min(value)

Specifies the earliest date allowed.

##### Parameters

1. `value` _(string)_ string representation of the oldest date allowed.

##### Example

```javascript
date.min('1970-01-01');
```

### <a name="datenullable" href="datenullable">#</a>date.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
date.nullable(true); // accepts nil values
```
