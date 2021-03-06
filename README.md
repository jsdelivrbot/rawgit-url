RawGit
===
[![NPM version][npm-image]][npm-url] [![Build Status][build-image]][build-url] [![Coverage Status][coverage-image]][coverage-url] [![Dependencies][dependencies-image]][dependencies-url]

> Get a [RawGit][rawgit] URL for a file hosted in a public Github repository.


## Installation

``` bash
$ npm install rawgit-url
```


## Usage

``` javascript
var rawgit = require( 'rawgit-url' );
```

#### rawgit( opts )

Returns a [RawGit][rawgit] URL for a file hosted in a public Github repository.

``` javascript
var opts = {
	'slug': 'math-io/erf/924ab65fcb2b2a2231808ae1cecad92570902a2e',
	'file': 'README.md'
};

var url = rawgit( opts );
// returns 'https://cdn.rawgit.com/math-io/erf/924ab65fcb2b2a2231808ae1cecad92570902a2e/README.md'
```

The `function` accepts the following `options`:
*	__slug__: public Github repository slug (*required*). The slug should include `owner` and `repo` information and should include either `commit`, `branch`, or `tag` information. For example,
	- `math-io/erf/924ab65fcb2b2a2231808ae1cecad92570902a2e`
	- `dstructs/array/develop`
	- ...etc.
*	__file__: filepath (*required*). For example,
	-	`lib/index.js`
	-	`./README.md`
	-	...etc.
*	__cdn__: `boolean` indicating whether to return a CDN URL. Default: `true`.

By default, the `function` returns a CDN URL. To return a (non-production) URL for development or testing, set the `cdn` option to `false`.

``` javascript
var opts = {
	'slug': 'dstructs/array/develop',
	'file': 'lib/index.js',
	'cdn': false
};

var url = rawgit( opts );
// returns 'https://rawgit.com/dstructs/array/develop/lib/index.js'
```


## Examples

``` javascript
var rawgit = require( 'rawgit-url' );

var opts = {
	'cdn': true,
	'slug': 'kgryte/rawgit-url/a9633f0dd2e3720dadedb965a30c999c2b0f8992',
	'file': 'README.md'
};

var url = rawgit( opts );

console.log( url );
// returns 'https://cdn.rawgit.com/kgryte/rawgit-url/a9633f0dd2e3720dadedb965a30c999c2b0f8992/README.md'
```

To run the example code from the top-level application directory,

``` bash
$ node ./examples/index.js
```


---
## CLI

### Installation

To use the module as a general utility, install the module globally

``` bash
$ npm install -g rawgit-url
```


### Usage

``` bash
Usage: rawgit [options] file

Options:

  -h,  --help               Print this message.
  -V,  --version            Print the package version.
       --no-cdn             Return a dev/testing URL.
       --slug slug          Github repository slug (should include branch, commit, 
                            or tag info).
```


### Notes

*	If not provided a `slug`, the module attempts to resolve a `slug` from a local `.git` repository located in the current working directory. The `slug` is a combination of `remote.origin.url` and the __current__ Git hash. For example,

	``` bash
	$ git config --get remote.origin.url
	# => https://github.com/kgryte/rawgit-url.git

	$ git rev-parse HEAD
	# => a9633f0dd2e3720dadedb965a30c999c2b0f8992
	```

	becomes

	``` javascript
	var slug = 'kgryte/rawgit-url/a9633f0dd2e3720dadedb965a30c999c2b0f8992';
	```


### Examples

``` bash
$ rawgit README.md --slug 'kgryte/rawgit-url/master'
# => https://cdn.jsdelivr.net/gh/kgryte/rawgit-url/README.md
```

To infer a Github repository `slug` from a local `.git` repository, omit the `slug` option.

``` bash
$ rawgit docs/img/eqn.svg
# => https://cdn.jsdelivr.net/gh/math-io/erf@924ab65fcb2b2a2231808ae1cecad92570902a2e/docs/img/eqn.svg
```


---
## Tests

### Unit

This repository uses [tape][tape] for unit tests. To run the tests, execute the following command in the top-level application directory:

``` bash
$ make test
```

All new feature development should have corresponding unit tests to validate correct functionality.


### Test Coverage

This repository uses [Istanbul][istanbul] as its code coverage tool. To generate a test coverage report, execute the following command in the top-level application directory:

``` bash
$ make test-cov
```

Istanbul creates a `./reports/coverage` directory. To access an HTML version of the report,

``` bash
$ make view-cov
```


### Browser Support

This repository uses [Testling][testling] for browser testing. To run the tests in a (headless) local web browser, execute the following command in the top-level application directory:

``` bash
$ make test-browsers
```

To view the tests in a local web browser,

``` bash
$ make view-browser-tests
```

<!-- [![browser support][browsers-image]][browsers-url] -->


---
## License

[MIT license](http://opensource.org/licenses/MIT).


## Copyright

Copyright &copy; 2016. Athan Reines.


[npm-image]: http://img.shields.io/npm/v/rawgit-url.svg
[npm-url]: https://npmjs.org/package/rawgit-url

[build-image]: http://img.shields.io/travis/kgryte/rawgit-url/master.svg
[build-url]: https://travis-ci.org/kgryte/rawgit-url

[coverage-image]: https://img.shields.io/codecov/c/github/kgryte/rawgit-url/master.svg
[coverage-url]: https://codecov.io/github/kgryte/rawgit-url?branch=master

[dependencies-image]: http://img.shields.io/david/kgryte/rawgit-url.svg
[dependencies-url]: https://david-dm.org/kgryte/rawgit-url

[dev-dependencies-image]: http://img.shields.io/david/dev/kgryte/rawgit-url.svg
[dev-dependencies-url]: https://david-dm.org/dev/kgryte/rawgit-url

[github-issues-image]: http://img.shields.io/github/issues/kgryte/rawgit-url.svg
[github-issues-url]: https://github.com/kgryte/rawgit-url/issues

[tape]: https://github.com/substack/tape
[istanbul]: https://github.com/gotwarlost/istanbul
[testling]: https://ci.testling.com

[rawgit]: http://rawgit.com/
