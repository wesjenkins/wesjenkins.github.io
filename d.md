# D

## Necessary Information

D is a compiled "systems" language with GC.

## General

```d
void main() {
	import std.stdio : writeln;
	
	writeln("Hello, World!");
	
	int x = 3;
	
	if (x > 0) {
		x = 5;
	} else if (x < 0) {
		x = -5;
	
	} else {
		x = 0;
	
	}
	
	foreach (i; 0..100) {
		x += 1;
	}
	
	while (x > 0) {
		x -= 1;
	}
}
```

## Types

### Built-in Types

```d
void main() {
	// Integer
	int x = 1;
	
	// Unsigned integer
	uint x = 1;
	
	// Float
	float y = 1.0;
	
	// Long
	long lx = 1L;
	
	// Boolean
	bool b = false;
	
	// Pointer to an integer
	int* p = &x;
	
	// Static array of integers
	int[3] xs = [1, 2, 3];
	
	// Dynamic array (slice) of integers
	int[] ys = [4, 5, 6];
}
```

### Using Structs

```d
struct Vec {
	int x;
	int y;
	int y;
	
	this(int x, int y, int z) {
		this.x = x;
		this.y = y;
		this.z = z;
	}
	
	auto opBinary(string s : "+")(const Vec rhs) {
		return Vec(x + rhs.x, y + rhs.y, z + rhs.z);
	}
	
	auto opBinary(string s : "*")(const Vec rhs) {
		return x * rhs.x + y * rhs.y + z * rhs.z;
	}
}

void main() {
	auto v1 = Vec(1, 2, 3);
	auto v2 = Vec(4, 5, 6);
	
	auto v3 = v1 + v2;
	
	auto dot = v1 * v3;
}
```

### Using Classes

```d
class Foo {
	this() {}
}

void main() {
	// Create new class instance
	Foo foo = new Foo();
	// Note that "new Foo" creates Foo, not Foo*
	// Class references are already pointers
}
```

## Common Tasks

### Type casting

```d
class Base {}

class Child : Base {}
class Child2 : Base {}

void main() {
	// Create an integer
	int x = 3;
	
	// Cast to float
	float y = cast(float)x;
	
	// Cast back to int
	int x2 = cast(int)y;
	
	assert(x == x2);
	// Of course, not true for all integers
	
	// Widening conversions are implicit
	long lx = x;
	double d = y;
	
	// And all pointers implicitly cast to void*
	void* ptr = &x;
	
	// Classes implicitly convert to parent class
	Base base = new Child();
	
	// Dynamically cast back to child
	Child child = cast(Child)base;
	
	// Incorrect dynamic casts will be null
	Child child2 = cast(Child2)base;
	asert(child2 is null);
}
```

### Memory management

```d
void main() {
	auto i = new int;
	auto xs = new int[5];
	
	// GC cleans up...
	
	// Can use any C memory management too
}
```

### String Manipulation

```d
void main() {
	// Create string
	// string is just immutable(char)[]
	auto s1 = "hello";
	// NOT null-terminated
	
	auto s2 = s1;
	
	// String compare
	assert(s1 == s2);
	
	// Append strings together
	auto s3 = s1 ~ s2;
	
	
}
```

### File IO

```d
char[] readFile(string filename) {
	import std.file;
	
	readText(filename);
}

void writeFile(string filename, void[] data) {
	import std.file;
	
	write(filename, data);
}

// More specific functions are in std.stdio
```

### Variable arguments

```d
// Declares a function which accepts an array
// or alternatively any number of arguments,
// which will construct an array
void printIntegers(int[] nums...) {
	import std.stdio;
	
	// Iterate over numbers
	foreach (num; nums) {
		// Print each number
		writeln(num);
	}
}

// Declares a template which accepts any arguments
void printValues(Ts...)(Ts vals) {
	import std.stdio;
	
	// Iterate over values
	foreach (val; vals) {
		// Print each one
		writeln(val);
	}
}
```

### Generating Random Numbers

```d
void main() {
	import std.random;
	
	// Generates an integer from [0, 10)
	auto x = uniform(0, 10);
	
	// Generates a float from [0, 1)
	auto f = uniform(0.0f, 1.0f);
}
```