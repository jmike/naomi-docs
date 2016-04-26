# Naomi singleton

## Table of Contents

* [Introduction](#introduction)
* [Methods](#methods)
  * [register(id, engine)](#register)
  * [create(engineId, [connectionProperties])](#create)

## Introduction

Naomi is a singleton. It's what you get when you load "naomi", e.g.

```javascript
var naomi = require('naomi');
```

Naomi is extensible. It allows registering external _database engines_ to handle different database types, e.g.

```javascript
var naomi = require('naomi');
var mysql = require('naomi-mysql');

naomi.register('mysql', mysql);
```

Once you have a database engine registered, you may use it to create a database instance, e.g.

```javascript
var db = naomi.create('mysql', {
  // connection properties
});
```

## Methods

### <a name="register" href="register">#</a>register(identifier, engine)

Registers the supplied database engine under the designated identifier.

##### Arguments

1. `identifier` _(string)_ database engine identifier, e.g. "mysql", "postgres".
2. `engine` _(Class\<Database\>)_ a Naomi Database.

##### Example

```javascript
var naomi = require('naomi');
var mysql = require('naomi-mysql');

// register mysql database class under "foobar"
naomi.register('foobar', mysql);
```

##### Note

The engine id is merely a string; you can call it whatever you want, e.g. "foobar" or "quux". It makes more sense, however, to name it according to the underlying database engine, e.g. "mysql" for MySQL.

### <a name="create" href="create">#</a>create(identifier, [connectionProperties]) -> [Database](database.md)

Creates and returns a new [Database](database.md) instance of the designated engine.

##### Arguments

1. `identifier` _(string)_ database engine identifier, e.g. "mysql", "postgres".
2. `connectionProperties` _(Object)_ connection properties specific to the database engine (optional).

##### Returns

Returns a new [Database](database.md) instance.

##### Example

```javascript
var naomi = require('naomi');
var mysql = require('naomi-mysql');

naomi.register('mysql', mysql);

var db = naomi.create('mysql', {
  host: process.env.MYSQL_HOST,
  port: parseInt(process.env.MYSQL_PORT, 10),
  user: process.env.MYSQL_USER,
  password: process.env.MYSQL_PASSWORD,
  database: process.env.MYSQL_DATABASE
});
```
