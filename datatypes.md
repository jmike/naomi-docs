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
* [enum](#enum)
  * [enum.default(value)](#enumdefault)
  * [enum.nullable(nullable)](#enumnullable)
  * [enum.values(values)](#enumvalues)
* [float](#float)
  * [float.default(value)](#floatdefault)
  * [float.max(limit)](#floatmax)
  * [float.min(limit)](#floatmin)
  * [float.negative(negative)](#floatnegative)
  * [float.nullable(nullable)](#floatnullable)
  * [float.positive(positive)](#floatpositive)
  * [float.precision(precision)](#floatprecision)
  * [float.scale(scale)](#floatscale)
* [integer](#integer)
  * [integer.autoinc(autoinc)](#integerautoinc)
  * [integer.default(value)](#integerdefault)
  * [integer.max(limit)](#integermax)
  * [integer.min(limit)](#integermin)
  * [integer.negative(negative)](#integernegative)
  * [integer.nullable(nullable)](#integernullable)
  * [integer.positive(positive)](#integernegative)
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
* [uuid](#uuid)
  * [uuid.default(value)](#uuiddefault)
  * [uuid.nullable(nullable)](#uuidnullable)

## binary

The _binary_ datatype is meant for storing binary data. It accepts [Buffer](https://nodejs.org/api/buffer.html) and string types (the latter being converted to Buffer internally).

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

The _boolean_ datatype is meant for storing boolean values. It accepts booleans, as well as the strings 'true', 'false', 'yes', 'no', 'on' or 'off'.

### <a name="booleannullable" href="booleannullable">#</a>boolean.nullable(nullable)

Marks the datatype as optional, which allows `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
boolean.nullable(true); // allows nil values
```


## date

The _date_ datatype is meant for storing date values. It accept JavaScript Date types, date-formatted strings and numbers (milliseconds since the epoch).

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

Specifies the date format.

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

The _email_ datatype is meant for storing email values. It accepts email-formatted strings.

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


## enum

The _enum_ datatype is meant for storing a set of predefined string values.

### <a name="enumvalues" href="enumvalues">#</a>enum.values(values)

Specifies allowed values.

##### Parameters

1. `values` _(Array<string>)_ an array of allowed values for this enumeration.

##### Example

```javascript
enum.values(['a', 'b', 'c']);
```

### <a name="enumdefault" href="enumdefault">#</a>enum.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(string, Function)_ the default value.

##### Example

```javascript
enum.default('a');
```

##### Notes

You may also specify a function to return the default value.

### <a name="enumnullable" href="enumnullable">#</a>enum.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
enum.nullable(true);
```


## float

The _float_ datatype is meant for storing float numbers.

### <a name="floatdefault" href="floatdefault">#</a>float.default(value)

Sets a default value if the original value is undefined.

##### Parameters

1. `default` _(number, Function)_ the default value.

##### Example

```javascript
float.default(12.34);
```

##### Notes

You may also specify a function to return the default value.

```javascript
float.default(Math.PI);
```

### <a name="floatmax" href="floatmax">#</a>float.max(limit)

Specifies the maximum allowed value.

##### Parameters

1. `limit` _(number)_ the maximum value allowed.

##### Example

```javascript
float.max(999.99);
```

### <a name="floatmin" href="floatmin">#</a>float.min(limit)

Specifies the minimum allowed value.

##### Parameters

1. `limit` _(number)_ the minimum value allowed.

##### Example

```javascript
float.min(-1.1);
```

### <a name="floatnegative" href="floatnegative">#</a>float.negative(negative)

If set to true requires value to be negative.

##### Parameters

1. `negative` _(boolean)_ whether the value is negative.

##### Example

```javascript
float.negative(true);
```

### <a name="floatnullable" href="floatnullable">#</a>float.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
float.nullable(true);
```

### <a name="floatpositive" href="floatpositive">#</a>float.positive(positive)

If set to true requires value to be positive.

##### Parameters

1. `positive` _(boolean)_ whether the value is positive.

##### Example

```javascript
float.positive(true);
```

### <a name="floatprecision" href="floatprecision">#</a>float.precision(precision)

Specifies the number of total digits allowed in value, including decimals.

##### Parameters

1. `precision` _(number)_ total digits allowed in value.

##### Example

```javascript
float.precision(5);
```

### <a name="floatscale" href="floatscale">#</a>float.scale(scale)

Specifies the number of decimal digits allowed in value.

##### Parameters

1. `precision` _(number)_ number of decimal digits allowed in value.

##### Example

```javascript
float.scale(2);
```


## integer

The _integer_ datatype is meant for storing integer numbers.

### <a name="integerautoinc" href="integerautoinc">#</a>integer.autoinc(autoinc)

If set to true marks value as automatically incremented. This has no effect in validation, but is essential to communicating with the database.

##### Parameters

1. `autoinc` _(boolean)_ whether the value is automatically incremented.

##### Example

```javascript
integer.autoinc(true);
```

### <a name="integerdefault" href="integerdefault">#</a>integer.default(value)

Sets a default value for this datatype.

##### Parameters

1. `value` _(number, Function)_ the default value.

##### Example

```javascript
integer.default(123);
```

##### Notes

You may also specify a function to return the default value, e.g.

### <a name="integermax" href="integermax">#</a>integer.max(limit)

Specifies the maximum allowed value.

##### Parameters

1. `limit` _(number)_ the maximum value allowed.

##### Example

```javascript
integer.max(999);
```

### <a name="integermin" href="integermin">#</a>integer.min(limit)

Specifies the minimum allowed value.

##### Parameters

1. `limit` _(number)_ the minimum value allowed.

##### Example

```javascript
integer.min(-100);
```

### <a name="integernegative" href="integernegative">#</a>integer.negative(negative)

If set to true requires value to be negative.

##### Parameters

1. `negative` _(boolean)_ whether the value is negative.

##### Example

```javascript
integer.negative(true);
```

### <a name="integernullable" href="integernullable">#</a>integer.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
integer.nullable(true);
```

### <a name="integerpositive" href="integerpositive">#</a>integer.positive(positive)

If set to true requires value to be positive.

##### Parameters

1. `positive` _(boolean)_ whether the value is positive.

##### Example

```javascript
integer.positive(true);
```


## string

The _string_ datatype is meant for storing strings.

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


## uuid

The _uuid_ datatype is meant for storing [Universal Unique Identifiers](https://en.wikipedia.org/wiki/Universally_unique_identifier).

### <a name="uuiddefault" href="uuiddefault">#</a>uuid.default(value)

Sets a default value if the original value is undefined.

##### Parameters

1. `default` _(string, Function)_ the default value.

##### Example

The following example assumes use of the notorious [node-uuid](https://github.com/broofa/node-uuid) library.

```javascript
var uuidGenerator = require('uuid');

uuid.default(uuidGenerator.v4);
```

### <a name="uuidnullable" href="uuidnullable">#</a>uuid.nullable(nullable)

Marks the datatype as optional, which allows the `undefined` and `null` values.

##### Parameters

1. `nullable` _(boolean)_ whether the datatype is nullable.

##### Example

```javascript
uuid.nullable(true); // accepts nil values
```
