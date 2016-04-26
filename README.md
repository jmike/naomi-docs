# Naomi

A simple ORM for Node.js that takes care of the repetitive CRUD tasks, while providing a handy interface for custom queries.

#### Features

* Accepts mongo-like query language to perform repretitive CRUD (+ count) tasks;
* Provides a handy interface for custom SQL queries;
* Leverages existing database meta-data instead of redefining the db schema in the application layer;
* Exposes promise and callback APIs.

## Installation

```
$ npm install naomi
```

#### Requirements

* Node.js 0.12+

#### Database engines currently available

1. [naomi-mysql](https://github.com/jmike/naomi-mysql)

## Philosophy

Databases, besides data, contain meta-data; stuff like...

* Column names + datatypes;
* Indices (primary keys, unique keys, etc);
* Constraints;
* Relations.

These metadata can be extracted from the database and are sufficient for generating basic validation rules and application structure. Yet most ORM tools tend to ignore database metadata and replicate that information in the application layer. This results to:

* **Unnecessary complexity**, i.e. you trade SQL with an ORM-specific API that is equally complex;
* **Synchronization issues**, i.e. the sky falls on your head when you change the db schema;
* **Reduced expressiveness**, i.e. no ORM can fully implement the expressiveness of SQL.

##### How is Naomi different?

Naomi works the other way around:

1. You first create the database using a tool of your choice, e.g. [MySQL Workbench](http://www.mysql.com/products/workbench/), [pgAdmin](http://www.pgadmin.org/) - a tool you already know;
2. You call a few simple methods to extract meta-information to the application layer.

While this approach may seem intriguing to new developers, it is in fact the natural way of thinking for experienced engineers. Creating a database requires creativity and imagination that machines lack. It is a task made for humans.

Naomi takes care of the SQL code by automating repetitive data queries. And if you need some custom logic you can always write it yourself.

## Acknowledgements

This project would not be without the extraordinary work of:

* Felix Geisendörfer (https://github.com/felixge/node-mysql)
* Brian C (https://github.com/brianc/node-postgres)
* Petka Antonov (https://github.com/petkaantonov/bluebird)

## Contribute

Source code contributions are most welcome. The following rules apply:

1. Follow the [Airbnb Style Guide](https://github.com/airbnb/javascript);
2. Make sure not to break the tests.

## License

MIT
