# Frequently Asked Questions

#### What's with the @#^%#& promises shit?

All Naomi methods expose both promises and callback interfaces. So you can do this:

```javascript
db.execute({ sql: 'SELECT 1;' }, function (err, records) {
  // do something with records
});
```

As well as this:

```javascript
db.execute({ sql: 'SELECT 1;' })
  .then(function (records) {
    // do something with records
  })
  .catch(function (err) {
    console.error(err);
  });
```

Choose the coding style that suits you best.

#### How do I connect to MySQL on Amazon RDS using SSL?

```javascript
var db = naomi.create('mysql', {
  host: 'host',
  port: 3306,
  user: 'user',
  password: 'password',
  database: 'schema',
  ssl: 'Amazon RDS'
});
```
