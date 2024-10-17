# Streams Module of NodeJS

Streams read a data from a source and pipe it to a destination.

- Streams is an `EventEmitter`
- implements special methods to make it the different types of streams

Usage:
- web application with lots of I/O operations
- live streaming of videos
- real time file uploads


## Types of Streams
- readable
    - used to read data from a source
    - stores data in internal buffer
    - by default the http module's `Request object` a readable stream

- writable
    - used to write data to the destination
    - stores data in internal buffer
    - by defailt the http module's `Response object` is a writable stream 

- duplex
    - used to read data from a source and write it to the destination


## Readable Streams

### Readabel Stream Methods

- `read()`
    - pulls data out of the internal buffer and returns it
- `setEnconding(encoding)`
    - returns strings of the specified encoding
- `resume()`
    - resumes emitting `data` events
- `stop()`
    - stopes emitting `data` events
- `pipe()`
    - pulls all data out of the readable stream
    - and writes it to the supplied destination


### Readable Stream Events

- `data` 
    - emitted when chunk of data flows in
- `readable`
    - emitted when the complete data is read into the internal buffer
- `end`
    - emitted when there will be no more data to read
- `close`
    - emitted when the stream is closed
- `error`
    - emitted when there is error received in the data


### Examples

#### using `data` event

```js
import fs from 'node:fs';

// create stream
const filePath = './test.txt';
const readStream = fs.createReadStream(filePath);

// read stream
let data = '';
// data is fired when chunks of data arrive into the internal buffer 
readStream.on('data', (chunk) => data += chunk);
readStream.on('end', () => console.log(data));
```

#### using `readable` event

```js
import fs from 'node:fs';

// create stream
const filePath = './test.txt';
const readStream = fs.createReadStream(filePath);

// read stream
let data = '';
let chunk;
// readable event is firead when all data is read into internal buffer
readStream.on('readable', () => {
    // while there is data in the internal buffer
    while( (chunk = readStream.read()) != null ) {
        // add it to the data variable
        data += chunk;
    } 
});

readStream.on('end', () => console.log(data));
```


## Writable Streams

### Writable Stream Methods

- `write()`
    - writes data to the destination
- `setDefaultEncoding(encoding)`
    - sets encoding for writeable stream
- `end()`
    - flushed data out of internal buffer
    - ends the stream

### Writable Stream Events

- `drain`
    - emitted when `stream.write(`) returns `false`
- `finish`
    - emitted when `s`tream.end()` method is invoked
- `pipe`
    - emitted when `stream.pipe()` method is invoked ona  `readable stream`
- `error`
    - emitted when there is an error writing data

### Writabel Stream Example

```js


