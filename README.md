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

#### Database engines currently available

1. [naomi-mysql](https://github.com/jmike/naomi-mysql)

## API Docs

* [Naomi singleton](naomi.md)
* [Database](database.md)
* [Schema](schema.md)
* [Collection](collection.md)

## Philosophy

Databases, besides data, contain meta-data; stuff like...

* Keys + datatypes
* Indices
* Constraints
* Relations

These meta-data can be extracted from the database and are sufficient for generating basic validation rules and application structure. Yet most ORM tools tend to ignore meta-data living in the database and replicate that information in the application layer, which results to:

* Unnecessary complexity, i.e. you trade a native query language (like SQL) with an ORM-specific API that is equally complex;
* Synchronization issues, i.e. the sky falls on your head every time you change the database schema;
* Reduced expressiveness, i.e. no ORM can fully implement the expressiveness of a native query language.

##### How is Naomi different?

Naomi works the boths ways:

###### Use case A

1. You first create the database using a tool of your choice, e.g. [MySQL Workbench](http://www.mysql.com/products/workbench/) or [pgAdmin](http://www.pgadmin.org/) - a tool you already know;
2. You call a simple method (namely [Collection#reverseEngineer()](collection.md#reverseEngineer)) to pull meta-information to the application layer.

While this approach may seem intriguing to new developers, it is in fact the natural way of thinking for experienced engineers. Creating a database requires creativity and imagination that machines lack. It is a task made for humans.

###### Use case B

1. You ;
2. You call a few simple methods to extract meta-information to the application layer.

In any case, naomi takes care of the SQL code by automating repetitive data queries. And if you need some custom logic you can always write it yourself.

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
