# Naomi

A simple ORM for Node.js that takes care of the repetitive CRUD tasks, while providing a handy interface for custom queries.

#### Features

* Accepts mongo-like query language to perform repretitive CRUD (+ count) tasks;
* Provides a handy interface for native queries, e.g. SQL;
* Leverages existing database meta-data instead of redefining the db schema in the application layer;
* Exposes promise and callback APIs.

## Installation

```
$ npm install naomi
```

#### Requirements

* Node.js 0.12+

#### Connectors currently available

| Connector | Maintainer | Build status | npm version |
|---|---|:---:|:---:|
| [naomi-mysql](https://github.com/jmike/naomi-mysql) | [jmike](https://github.com/jmike) | [![Build Status](https://travis-ci.org/jmike/naomi-mysql.svg?branch=master)](https://travis-ci.org/jmike/naomi-mysql) | [![npm version](https://badge.fury.io/js/naomi-mysql.svg)](https://badge.fury.io/js/naomi-mysql) |

## API Docs

* [Naomi singleton](naomi.md)
* [Database](database.md)
* [Schema](schema.md)
* [Collection](collection.md)

## Philosophy

Databases, besides data, contain meta-data; stuff like `keys`, `datatypes`, `indices`, `constraints` and `relations`.

These meta-data can be extracted from the database and are sufficient for generating basic validation rules and application structure. Yet most ORM tools tend to ignore meta-data living in the database and replicate that information in the application layer, which results to:

* Unnecessary complexity, i.e. you trade a native query language (like SQL) with an ORM-specific API that is equally complex;
* Synchronization issues, i.e. the sky falls on your head every time you change the database schema;
* Reduced expressiveness, i.e. no ORM can fully implement the expressiveness of a native query language.

##### How is Naomi different?

Naomi is different in 2 ways:

1. It provides methods to run repetitive CRUD (+ count) operations using a familiar mongo-like query language. When that's not enough it allows you run native queries directly to the database.
2. It exposes simple methods to extract meta-data from the database, thus eliminating the need to recreate the information in the application layer and putting you (not the ORM) in charge of your schema.

With Naomi you have the freedom to create the database using a tool of your choice, e.g. [MySQL Workbench](http://www.mysql.com/products/workbench/) or [pgAdmin](http://www.pgadmin.org/). While this approach may seem intriguing to new developers, it is in fact the natural way of thinking for experienced engineers. Creating a database requires creativity and imagination that machines lack. It is a task made for humans.

## Acknowledgements

This project would not be without the extraordinary work of:

* Nicolas Morel (https://github.com/hapijs/joi)
* Petka Antonov (https://github.com/petkaantonov/bluebird)
* Felix Geisendörfer (https://github.com/felixge/node-mysql)

## Contribute

Source code contributions are most welcome. The following rules apply:

1. Follow the [Airbnb Style Guide](https://github.com/airbnb/javascript);
2. Make sure not to break the tests.

## License

MIT
