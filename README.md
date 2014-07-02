flow-pcc
========

Reduce transform stream which computes the [Pearson product-moment correlation coefficient (PCC)](http://en.wikipedia.org/wiki/Pearson_coefficient) of a numeric data stream.


## Installation

``` bash
$ npm install flow-pcc
```


## Examples

``` javascript
var eventStream = require( 'event-stream' ),
	cStream = require( 'flow-pcc' );

// Create some data... (negatively corrrelated)
var data = new Array( 1000 ), value;
for ( var i = 0; i < data.length; i++ ) {
	value = Math.random() * 50;
	data[ i ] = {
		'y1': 50 + value,
		'y2': 50 - value
	}
}

// Create a readable stream:
var readStream = eventStream.readArray( data );

// Create a new stream:
var stream = cStream()
	.accessors( 'y1', function( d ) {
		return d.y1;
	})
	.accessors( 'y2', function( d ) {
		return d.y2;
	})
	.stream();

// Pipe the data:
readStream.pipe( stream )
	.pipe( eventStream.stringify() )
	.pipe( process.stdout );
```

## Tests

Unit tests use the [Mocha](http://visionmedia.github.io/mocha) test framework with [Chai](http://chaijs.com) assertions.

Assuming you have installed Mocha, execute the following command in the top-level application directory to run the tests:

``` bash
$ mocha
```

All new feature development should have corresponding unit tests to validate correct functionality.


## License

[MIT license](http://opensource.org/licenses/MIT). 


---
## Copyright

Copyright &copy; 2014. Athan Reines.

