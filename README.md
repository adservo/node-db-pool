# db-pool [![Build Status](https://secure.travis-ci.org/mark/node-db-pool.png?branch=master)](http://travis-ci.org/mark/node-db-pool)

Easily create a Postgres/MySQL connection pool (postgres only until I get MariaDB/MySQL working on my new Ubuntu 13.04 dev machine).

Behind the scenes it returns an any-db pool which can be used as described (https://github.com/grncdr/node-any-db)[here].

## Getting Started
Install the module with: `npm install db-pool`

## Configuration
Create a config/database.js containing something like
```javascript
exports.postgres = {
  defaults: {
    min: 5,
    max: 20
  },
  development: {
    database: "development",
    username: "username",
    password: "pass"
  },
  production: {
    database: "production",
    username: "username",
    password: "pass",
    port: 9999
  },
  test: {
    database: "test",
    username: "username",
    password: "pass",
    host: "some.hostname",
    min: 15
  }
};
```

## Example
```javascript
var db_pool = require('db-pool');

// Optionally specify an alternative config file (default is to use /config/database.js)
db_pool.load('/config/custom-db-config-file.js');

// Create a pool to a development database
var dev = db_pool.pool('development'); // or db_pool.pool('postgres.development');

// Create another pool to a different database
var test = db_pool.pool('test');

// Show the known connections. Active ones have pool, connStr and merged default attributes.
console.log(db_pool.debug());

// Run a query
dev.query("SELECT 1", function (err, results) {
  console.log(results);

  // Terminate all active pools
  db_pool.closeAll();
})

```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_

## License
Copyright (c) 2013 Mark Selby  
Licensed under the MIT license.
