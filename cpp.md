# C++

## Necessary Information

C++ is a compiled "systems" language.

## General

```cpp
// Note lack of .h
#include <iostream>

int main() {
	std::cout << "Hello, World!" << std::endl;
	
	int x = 3;
	
	if (x > 0) {
		x = 5;
	} else if (x < 0) {
		x = -5;
	
	} else {
		x = 0;
	
	}
	
	for (int i = 0; i < 100; ++i) {
		x += 1;
	}
	
	while (x > 0) {
		x -= 1;
	}

	return 0;
}
```

## Types

### Built-in Types

```cpp
#include <cassert>

int main() {
	// Integer
	int x = 1;
	
	// Unsigned integer
	unsigned int x = 1;
	
	// Float
	float y = 1.0;
	
	// Long
	long lx = 1L;
	
	// Long long
	long long llx = 1LL;
	
	// Booleans
	bool b = true;
	
	// Pointer to an integer
	int* p = &x;
	
	// LValue reference to an integer
	int& r = x;
	
	// RValue reference to an integer
	int&& r2 = x;
	
	// Static array of integers
	int xs[3] = { 1, 2, 3 };
	int ys[]  = { 4, 5, 6 };
	
	return 0;
}
```

### Using Structs

```cpp
struct Vec {
	// Fields are default public in structs
	int x;
	int y;
	int z;
	
	// Methods
	
	// Constructor
	Vec(int x, int y, int z) {
		// Implicit this variable
		this->x = x;
		this->y = y;
		this->z = z;
	}
	
	// Deconstructor
	~Vec() { }
	
	// Operator overloading
	Vec operator +(const Vec&& rhs) {
		return Vec(x + rhs.x, y + rhs.y, z + rhs.z);
	}
	
	int operator *(const Vec&& rhs) {
		return x * rhs.x + y * rhs.y + z * rhs.z;
	}
};

int main(void) {
	// Call constructor
	Vec x = Vec(1, 2, 3);
	
	// Universal construction syntax
	Vec y {1, 2, 3};
	
	// Use operator overloads
	Vec z = x + y;
	
	int q = z * y;
	
	// Access struct field
	std::cout << "Value: " << z.x << std::endl;
	
	return 0;
}

```

## Common Tasks

### Type Casting

```cpp
#include <cassert>

class Base {}

class Child : Base {}

int main() {
	// Create an integer
	int x = 3;
	
	// Cast to float
	float y = static_cast<float>(x);
	
	// Cast back to int
	int x2 = static_cast<int>(y);
	
	assert(x == x2);
	// Of course, not true for all integers
	
	// Reinterpret the same int bit pattern as a float
	float z = reinterpret_cast<float&>(x);
	
	// Pointers implicitly convert to parent class
	Base* ptr = new Child();

	// Dynamic cast back to child
	Child* ptr2 = dynamic_cast<Child*>(ptr):
	
	// And it will be null if it's the wrong type
	assert(ptr2 != nullptr);
	
	return 0;
}
```

### Memory management

```cpp
// Required to use unique and shared pointers
#include <memory>

struct Foo {
	int x;

    Foo(int x) {
        this->x = x;
    }
};

int main() {
	// Create and delete Foo object
	Foo* foo = new Foo();
	delete foo;
	
	// Create an array of Foo objects
	foo = new Foo[16];
	delete[] foo;
	// Remember to use delete[] !
	
	// Makes a unique pointer that handles clean-up using RAII
	auto p1 = std::make_unique<Foo>(3);
	
	// unique pointer only moves, never copies
	// auto p2 = p1; // doesn't compile
	
	// Force p1 to move to p2, p1 now invalid
	auto p2 = std::move(p1);
	
	// Access value stored
	std::cout << *p2 << std::endl;
	
	// Create a shared pointer which is the same, except reference counted
	auto p3 = std::make_shared<Foo>(5);
	
	// Allowed
	auto p4 = p3;
	
	// Access the same way
	std::cout << *p4 << std::endl;
	
	return 0;
}
```

### String Manipulation

```cpp
#include <string>
#include <cassert>

int main() {
	// Create opaque string object
	std::string s = "hello";
	
	// Append to string
	s += " there;";
	
	// Remove final character
	s.pop_back();
	
	// Compare strings using normal equality operators
	assert(s == s);
	
	// Create substring of first 5 characters
	auto s2 = s.substr(0, 5);
	// Note: The second argument is the substring length!
	//       Not the ending index
	
	// Find substring inside string
	auto index = s1.find(s2);
	assert(index == 0);
	
	index = s1.find("not there");
	assert(index == std::string::npos);
	
	return 0;
}
```

### File IO

```cpp
#include <fstream>
#include <string>

std::string readFile(std::string filename) {
	// Open file
	std::ifstream fp { filename };
	
	// Insert error handling here
	if (!fp.is_open())
		return std::string();
	
	// Create empty string
	std::string data;
	
	// Read file data
	fp >> data;
	
	// Return data
	return data;
	// Can do: return std::move(data);
	//         But a good compiler should do this
	//         Not recommended to write yourself
	
	// File automatically closed when ifstream is destroyed 
}

void writeFile(std::string filaname, std::string data) {
	// Open file
	std::ofstream fp { filename };
	
	// Insert error handling here
	if (!fp.is_open())
		return;
	
	// Write data to fp
	fp << data;
	
	// File automatically closed when ofstream is destroyed 
}
```

### Variable arguments

```cpp
#include <iostream>

// Using recursive style

// Empty base case
inline void printIntegers() {}

// Recursive template case
template <typename... Ints>
inline void printIntegers(int first, Ints... rest)
{
	// First, print first
	std::cout << first << std::endl;
	
	// Then, recursively print the rest
	printIntegers2(rest...);
}

int main() {
	// Call variable argument function
	printIntegers(0, 1, 2);
	printIntegers(0, 1);
	// They're called the same way as any other
	// No need to pass the length to a variadic template
	
	return 0;
}
```

### Generating Random Numbers

```cpp
#include <random>

std::mt19937 rand;

int main() {
	// Access some outside entropy
	std::random_device rd;
	
	// And create a random generator
	// with a random seed
	rand = std::mt19937(rd);
	
	// Create a uniform integer distribution from [0, 128)
	std::uniform_int_distribution<int> intDist { 0, 128 };
	
	// Call distribution with a generator to generate a number
	std::cout << "Got (int): " << intDist(rand) << std::endl;
	
	// Create a uniform float distribution from [0, 1)
	std::uniform_real_distribution<float> floatDist { 0.0f, 1.0f };
	
	std::cout << "Got (float): " << floatDist(rand) << std::endl;
	
	// Create a normal distribution with mean = 0, stdev = 1.0
	std::normal_distribution<double> normDist { 0.0, 1.0 };
	
	std::cout << "Got (normal): " << normDist(rand) << std::endl;
	
	return 0;
}

```