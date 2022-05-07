# Javascript

## Necessary Information

Javascript is an interpreted multi-paradigm language commonly used in web browsers.

## General

```js
// Semicolons optional, but recommended

// Function says hello
function sayHello() {
	console.log("Hello, World!");
	
	// Create local
	let x = 3;
	
	if (x > 0) {
		x = 5;
	
	} else if (x < 0) {
		x = -5;
		
	} else {
		x = 0;
	}
	
	for (let i = 0; i < 100; ++i) {
		x += 1;
	}
	
	while (x > 0) {
		x -= 1;
	}
	
	obj = { a: 1, b: 2 };
	
	// for..of loop
	for (const [key, val] of obj) {
		console.log(key, " = ", val);
	}
}
```

## Types

### Built-in Types

```js
// Number
x = 1
console.assert(typeof(x) == "number")

x = 1.0
console.assert(typeof(x) == "number")

// Boolean
x = true
console.assert(typeof(x) == "boolean")

// Objects can be arrays or dictionaries
// (In fact, they're the same)
x = [1, 2]
console.assert(typeof(x) == "object")

x = {x: 1, y: 2}
console.assert(typeof(x) == "object")
```

## Common Tasks

### List manipulation

```js
xs = [1, 2, 3, 4]

// Sort in place
xs.sort()

// Reverse in place
xs.reverse()
```

### String Manipulation

```js
// Create a string
s1 = "hi there"

// Split string
xs = s1.split(" ")

// Join string
s2 = xs.join(" ")

console.assert(s1 == s2)
```

### Generating Random Numbers

```js
// Random number from [0, 1)
x = math.random()

// Random integer from [0, n)
x = math.floor(math.random() * n)
```