# Node.JS

## Necessary Information

Node.JS is a Javascript runtime environment to run Javascript outside a browser.
Of course, the language is just Javascript.
So, syntax help is [here](https://wesjenkins.github.io/javascript).

## File System

### File IO

```js
// Import file system functions
import { readFile, writeFile } from 'node:fs/promises';
// (Note, can only use import inside a module!)

const inFile = 'from.txt';
const outfile = 'to.txt';

// Read from file and wait
const data = await readFile(inFile);

// Write to file and wait
await writeFile(outFile, data);
```

## HTTP

### Basic HTTP Server

```js
// Import http module
const http = require('http')

const hostname = '127.0.0.1'
const port = 3000

// Request callback called with request and response objects
const server = http.createServer((req, res) => {
	// Set response status code and header
	res.statusCode = 200
	res.setHeader('Content-Type', 'text/plain')
	
	// And set response body
	res.end('Hello World\n')
})

// Then, listen on hostname:port
server.listen(port, hostname, () => {
	// Callback called when listening starts
	console.log(`Server running at http://${hostname}:${port}/`)
})
```