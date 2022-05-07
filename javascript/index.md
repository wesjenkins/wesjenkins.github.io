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
	
	// Create object
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

// undefined
x = undefined;

// undefined is the result when a key doesn't exist
console.assert(x === {1: 3}[5]);
```

### Old-Style Classes

```js
function Vec(x, y, z) {
	this.x = x;
	this.y = y;
	this.z = z;
}

Vec.prototype.add = function(rhs) {
	return Vec(this.x + rhs.x, this.y + rhs.y, this.z + rhs.z);
}

Vec.prototype.dot = function(rhs) {
	return this.x * rhs.x + this.y * rhs.y + this.z * rhs.z;
}

let v1 = new Vec(1, 2, 3);
let v2 = new Vec(4, 5, 6);

let v3 = v1.add(v2);

let dot = v1.dot(v3);
```

### New-Style Classes (ES6)

```js
class Vec {
	// Constructor method
	constructor(x, y, z) {
		this.x = x;
		this.y = y;
		this.z = z;
	}
	
	// Overload to string
	toString() {
		// Interpolated string
		return `(${this.x}, ${this.y}, ${this.z})`;
	}
	
	// No fancy operator overloading
	add(rhs) {
		return new Vec(this.x + rhs.x, this.y + rhs.y, this.z + rhs.z);
	}
	
	dot(rhs) {
		return this.x * rhs.x + this.y * rhs.y + this.z * rhs.z;
	}
}

let v1 = new Vec(1, 2, 3);
let v2 = new Vec(4, 5, 6);

let v3 = v1.add(v2);

let dot = v1.dot(v3);
```

### Proxy Objects

```js
let data = {x: 1, y: 2};

// Proxy objects
// Similar to Lua metatables
let p = new Proxy(data, {
	// Customize get behavior
	get(obj, prop) {
		// If it exists, return it using Reflect
		if (data[obj] !== undefined)
			return Reflect.get(obj, prop);
		else
			return 0;
		// But default to 0
	},
	
	// Customize set behavior
	set(obj, prop, newval) {
		// Only allow setting if it already exists
		if (data[obj] !== undefined)
			Reflect.set(obj, prop, newval);
	},
});
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