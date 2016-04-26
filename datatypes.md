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
* [email](#email)
  * [email.default(value)](#emaildefault)
  * [email.length(limit)](#emaillength)
  * [email.lowercase(lowercase)](#emaillowercase)
  * [email.maxLength(limit)](#emailmaxlength)
  * [email.minLength(limit)](#emailminlength)
  * [email.nullable(nullable)](#emailnullable)
  * [email.trim(trim)](#emailtrim)
  * [email.uppercase(uppercase)](#emailuppercase)
* [string](#string)
  * [string.default(value)](#stringdefault)
  * [string.length(limit)](#stringlength)
  * [string.lowercase(lowercase)](#stringlowercase)
  * [string.maxLength(limit)](#stringmaxlength)
  * [string.minLength(limit)](#stringminlength)
  * [string.nullable(nullable)](#stringnullable)
  * [string.regex(regex)](#stringregex)
  * [string.trim(trim)](#stringtrim)
  * [string.uppercase(uppercase)](#stringuppercase)

## binary

The _binary_ datatype matches [Buffer](https://nodejs.org/api/buffer.html) and string types (the latter being converted to Buffer internally).

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

The _boolean_ datatype matches boolean types (as well as the strings 'true', 'false', 'yes', 'no', 'on' or 'off').

### <a name="booleannullable" href="booleannullable">#</a>boolean.nullable(nullable)

Marks the datatype as optional, which allows `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
boolean.nullable(true); // allows nil values
```


## date

The _date_ datatype matches JavaScript Date types, date strings and number of milliseconds.

### <a name="datedefault" href="datedefault">#</a>date.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(string, Date, Function)_ the default value.

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


## email

The _email_ datatype matches email types.

### <a name="emaildefault" href="emaildefault">#</a>email.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(email, Function)_ the default value.

##### Example

```javascript
email.default('abc');
```

##### Notes

You may also specify a function to return the default value.

### <a name="emaillength" href="emaillength">#</a>email.length(limit)

Specifies the exact email length required.

##### Parameters

1. `limit` _(number)_ the exact email length required.

##### Example

```javascript
email.length(3);
```

### <a name="emaillowercase" href="emaillowercase">#</a>email.lowercase(lowercase)

Requires the email value to be all lowercase.

##### Parameters

1. `lowercase` _(boolean)_ whether the email value is all lowercase.

##### Example

```javascript
email.lowercase(true);
```

### <a name="emailuppercase" href="emailuppercase">#</a>email.uppercase(uppercase)

Requires the email value to be all uppercase.

##### Parameters

1. `uppercase` _(boolean)_ whether the email value is all uppercase.

##### Example

```javascript
email.uppercase(true);
```

### <a name="emailmaxlength" href="emailmaxlength">#</a>email.maxLength(limit)

Specifies the maximum number of email characters allowed.

##### Parameters

1. `limit` _(number)_ the maximum number of email characters allowed.

##### Example

```javascript
email.maxLength(5);
```

### <a name="emailminlength" href="emailminlength">#</a>email.minLength(limit)

Specifies the minimum number of email characters allowed.

##### Parameters

1. `limit` _(number)_ the minimum number of email characters allowed.

##### Example

```javascript
email.minLength(1);
```

### <a name="emailnullable" href="emailnullable">#</a>email.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
email.nullable(true); // accepts nil values
```

### <a name="emailtrim" href="emailtrim">#</a>email.trim(trim)

Requires the email value to contain no whitespace before or after.

##### Parameters

1. `trim` _(boolean)_ whether the value allows whitespace before or after.

##### Example

```javascript
email.trim(true);
```


## string

The _string_ datatype matches string types.

### <a name="stringdefault" href="stringdefault">#</a>string.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(string, Function)_ the default value.

##### Example

```javascript
string.default('abc');
```

##### Notes

You may also specify a function to return the default value.

### <a name="stringlength" href="stringlength">#</a>string.length(limit)

Specifies the exact string length required.

##### Parameters

1. `limit` _(number)_ the exact string length required.

##### Example

```javascript
string.length(3);
```

### <a name="stringlowercase" href="stringlowercase">#</a>string.lowercase(lowercase)

Requires the string value to be all lowercase.

##### Parameters

1. `lowercase` _(boolean)_ whether the string value is all lowercase.

##### Example

```javascript
string.lowercase(true);
```

### <a name="stringuppercase" href="stringuppercase">#</a>string.uppercase(uppercase)

Requires the string value to be all uppercase.

##### Parameters

1. `uppercase` _(boolean)_ whether the string value is all uppercase.

##### Example

```javascript
string.uppercase(true);
```

### <a name="stringmaxlength" href="stringmaxlength">#</a>string.maxLength(limit)

Specifies the maximum number of string characters allowed.

##### Parameters

1. `limit` _(number)_ the maximum number of string characters allowed.

##### Example

```javascript
string.maxLength(5);
```

### <a name="stringminlength" href="stringminlength">#</a>string.minLength(limit)

Specifies the minimum number of string characters allowed.

##### Parameters

1. `limit` _(number)_ the minimum number of string characters allowed.

##### Example

```javascript
string.minLength(1);
```

### <a name="stringnullable" href="stringnullable">#</a>string.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
string.nullable(true); // accepts nil values
```

### <a name="stringregex" href="stringregex">#</a>string.regex(regex)

Specifies a regular expression rule to validate values against.

##### Parameters

1. `regex` _(string, RegExp)_ a regular expression rule.

##### Example

```javascript
string.regex(/^[abc]+$/);
```

### <a name="stringtrim" href="stringtrim">#</a>string.trim(trim)

Requires the string value to contain no whitespace before or after.

##### Parameters

1. `trim` _(boolean)_ whether the value allows whitespace before or after.

##### Example

```javascript
string.trim(true);
```
