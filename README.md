# array-sort [![NPM version](https://badge.fury.io/js/array-sort.svg)](http://badge.fury.io/js/array-sort)

> Fast and powerful array sorting. Sort an array of objects by one or more properties. Any number of nested properties or custom comparison functions may be used.

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i array-sort --save
```

## Usage

Sort an array by the given object property:

```js
var arraySort = require('array-sort');

arraySort([{foo: 'y'}, {foo: 'z'}, {foo: 'x'}], 'foo');
//=> [{foo: 'x'}, {foo: 'y'}, {foo: 'z'}]
```

**Reverse order**

```js
arraySort([{foo: 'y'}, {foo: 'z'}, {foo: 'x'}], 'foo', {reverse: true});
//=> [{foo: 'z'}, {foo: 'y'}, {foo: 'x'}]
```

## Table of contents

<!-- toc -->

* [Params](#params)
* [Examples](#examples)
* [Related projects](#related-projects)
* [Running tests](#running-tests)
* [Contributing](#contributing)
* [Author](#author)
* [License](#license)

_(Table of contents generated by [verb](https://github.com/assemble/verb))_

<!-- tocstop -->

## Params

```js
arraySort(array, comparisonArgs);
```

* `array`: **{Array}** The array to sort
* `comparisonArgs`: **{Function|String|Array}**: One or more functions or object paths to use for sorting.

## Examples

**[Sort blog posts](examples/blog-posts.js)**

```js
var arraySort = require('array-sort');

var posts = [
  { path: 'c.md', locals: { date: '2014-01-09' } },
  { path: 'a.md', locals: { date: '2014-01-02' } },
  { path: 'b.md', locals: { date: '2013-05-06' } },
];

// sort by `locals.date`
console.log(arraySort(posts, 'locals.date'));

// sort by `path`
console.log(arraySort(posts, 'path'));
```

**[Sort by multiple properties](examples/multiple-props.js)**

```js
var arraySort = require('array-sort');

var posts = [
  { locals: { foo: 'bbb', date: '2013-05-06' }},
  { locals: { foo: 'aaa', date: '2012-01-02' }},
  { locals: { foo: 'ccc', date: '2014-01-02' }},
  { locals: { foo: 'ccc', date: '2015-01-02' }},
  { locals: { foo: 'bbb', date: '2014-06-01' }},
  { locals: { foo: 'aaa', date: '2014-02-02' }},
];

// sort by `locals.foo`, then `locals.date`
var result = arraySort(posts, ['locals.foo', 'locals.date']);

console.log(result);
// [ { locals: { foo: 'aaa', date: '2012-01-02' } },
//   { locals: { foo: 'aaa', date: '2014-02-02' } },
//   { locals: { foo: 'bbb', date: '2013-05-06' } },
//   { locals: { foo: 'bbb', date: '2014-06-01' } },
//   { locals: { foo: 'ccc', date: '2014-01-02' } },
//   { locals: { foo: 'ccc', date: '2015-01-02' } } ]
```

**[Custom function](examples/custom-function.js)**

If custom functions are supplied, array elements are sorted according to the return value of the compare function. See the [docs for ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)`Array.sort()` for more details.

```js
var arr = [
  {one: 'w', two: 'b'},
  {one: 'z', two: 'a'},
  {one: 'x', two: 'c'},
  {one: 'y', two: 'd'},
];

function compare(prop) {
  return function (a, b) {
    return a[prop].localeCompare(b[prop]);
  };
}

var result = arraySort(arr, function (a, b) {
  return a.two.localeCompare(b.two);
});

console.log(result);
// [ { one: 'z', two: 'a' },
//   { one: 'w', two: 'b' },
//   { one: 'x', two: 'c' },
//   { one: 'y', two: 'd' } ]
```

**[Multiple custom functions](examples/custom-functions.js)**

```js
var arr = [
  {foo: 'w', bar: 'y', baz: 'w'},
  {foo: 'x', bar: 'y', baz: 'w'},
  {foo: 'x', bar: 'y', baz: 'z'},
  {foo: 'x', bar: 'x', baz: 'w'},
];

// reusable compare function
function compare(prop) {
  return function (a, b) {
    return a[prop].localeCompare(b[prop]);
  };
}

// the `compare` functions can be a list or array
var result = arraySort(arr, compare('foo'), compare('bar'), compare('baz'));

console.log(result);
// [ { foo: 'w', bar: 'y', baz: 'w' },
//   { foo: 'x', bar: 'x', baz: 'w' },
//   { foo: 'x', bar: 'y', baz: 'w' },
//   { foo: 'x', bar: 'y', baz: 'z' } ]
```

## Related projects

* [get-value](https://github.com/jonschlinkert/get-value): Use property paths (`  a.b.c`) to get a nested value from an object.
* [sort-asc](https://github.com/jonschlinkert/sort-asc): Sort array elements in ascending order.
* [sort-desc](https://github.com/jonschlinkert/sort-desc): Sort array elements in descending order.
* [set-value](https://github.com/jonschlinkert/set-value): Create nested values and any intermediaries using dot notation (`'a.b.c'`) paths.
* [sort-object](https://github.com/doowb/sort-object): Sort the keys in an object.

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/array-sort/issues/new)

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on July 18, 2015._