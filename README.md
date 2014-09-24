# JohnnyCache

MongoDB standalone caching library for Node.js. It is a fork of [cacheman-mongo](https://travis-ci.org/cayasso/cacheman-mongo).
The main difference between JohnnyCache and the original Cacheman is that JohnnyCache can be configured with a Mongo connection string.

Also, I cleaned up the code a little bit.

## Installation

``` bash
$ npm install johnny-cache
```

## Usage

```javascript
var JohnnyCache = require('johnny-cache');
var cache = new JohnnyCache();

// set the value
cache.set('my key', { foo: 'bar' }, function (error) {

  if (error) throw error;

  // get the value
  cache.get('my key', function (error, value) {

    if (error) throw error;

    console.log(value); //-> {foo:"bar"}

    // delete entry
    cache.del('my key', function (error){
      
      if (error) throw error;

      console.log('value deleted');
    });

  });
});
```

## API

### JohnnyCache([options])

Create `johnny-cache` instance. `options` is a map, with db and collection properties.

```javascript
var options = { 
  db: 'mongo://localhost/mymongo',
  collection: 'my-collection'
};

var cache = new JohnnyCache(options);
```

### cache.set(key, value, [ttl, [fn]])

Stores or updates a value.

```javascript
cache.set('foo', { a: 'bar' }, function (err, value) {
  if (err) throw err;
  console.log(value); //-> {a:'bar'}
});
```

Or add a TTL(Time To Live) in seconds like this:

```javascript
// key will expire in 60 seconds
cache.set('foo', { a: 'bar' }, 60, function (err, value) {
  if (err) throw err;
  console.log(value); //-> {a:'bar'}
});
```

### cache.get(key, fn)

Retreives a value for a given key, if there is no value for the given key a null value will be returned.

```javascript
cache.get(function (err, value) {
  if (err) throw err;
  console.log(value);
});
```

### cache.del(key, [fn])

Deletes a key out of the cache.

```javascript
cache.del('foo', function (err) {
  if (err) throw err;
  // foo was deleted
});
```

### cache.clear([fn])

Clear the cache entirely, throwing away all values.

```javascript
cache.clear(function (err) {
  if (err) throw err;
  // cache is now clear
});
```

## Run tests

``` bash
$ make test
```

## License

(The MIT License)

Copyright (c) 2014 Terrence C. Watson &lt;terrence.watson@contractor.cengage.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
