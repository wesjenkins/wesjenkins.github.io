# C#

## Necessary Information

C# is a popular compiled/interpreted language.

## General

```cs
using System;

// Everything must live inside a class
class Test
{
	static void Main() {
		Console.WriteLine("Hello, World!");
		
		var x = 3;
	
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
	}
}
```

## Types

### Built-in Types

```cs
class Test
{
	static void Main() {
		// Integers and longs
		int x = 1;
		long w = 13;
		
		// Floats and doubles
		float f = 1.0f;
		double z = 1.0;
		
		// Strings
		string s = "hi!";
		
		// Arrays
		int[] xs = { 1, 2, 3, 4 };
	}
}
```

### Classes

```cs
// Define class
class Vector
{
	int x;
	int y;
	int z;
	
	// Default is private
	public Vector(int x, int y, int z) {
		this.x = x;
		this.y = y;
		this.z = z;
	}
	
	// Override toString method
	public override string ToString() {
		return String.Format("({0}, {1}, {2})", x, y, z);
	}
	
	// Operator overloading
	public static Vector operator +(Vector lhs, Vector rhs) {
	    return new Vector(lhs.x + rhs.x, lhs.y + rhs.y, lhs.z + rhs.z);
	}
	
	public static Vector operator *(Vector lhs, Vector rhs) {
	    return lhs.x * rhs.x + lhs.y * rhs.y + lhs.z * rhs.z;
	}
}

class Test
{
	static void Main() {
		// Create objects
		var v1 = new Vector(1, 2, 3);
		var v2 = new Vector(4, 5, 6);
		
		// Use methods
		var v3 = v1 + v2;
		var dot = v1 * v3;
	}
}
```

## Common Tasks

### Type Casting

```cs
class Base {}
class Child : Base {}
class Child2 : Base {}

class Test
{
	static void Main() {
		// Create an integer
		int x = 3;
		
		// Cast to float
		float y = (float)x;
		
		// Cast back to int
		int x2 = (int)y;
		
		// Classes implicitly convert to parent class
		Base b = new Child();
		
		// Cast back to child class dynamically
		Child child = (Child)b;
		
		// This will throw a runtime error
		// Child2 child2 = (Child2)b;
	}
}
```

### List Manipulation

```cs
using System.Collections.Generic;

class Test
{
	static void Main() {
		// Create an array
		int[] arr = { 1, 2, 3, 4 };
		
		// Convert array to list
		List<int> list = new List<int>(arr);
		
		// Index like an array
		int val = arr[0];
		arr[0] = 3;
		
		// Add a new integer to the end
		list.Add(new Integer(5));
	}
}
```

### String Manipulation

```cs
using System;
using System.Diagnostics;

class Test
{
	static void Main() {
		// Create a strings
		string s = "hello";
		string s2 = " there";
		
		// Add strings together
		string s3 = s + s2;
		
		// Create a substring
		string sub = s3.Substring(0, 5);
		
		// String equality
		Debug.Assert(s == sub);
		
		// Substring search
		Debug.Assert(s3.IndexOf("there") == 6);
		
		Debug.Assert(s3.IndexOf("asdf") == -1);
	}
}
```

### Basic File IO

```java
using System;
using System.IO;
using System.Text;

// Obviously, there's more complex IO available
// I'm being lazy
// Just reading, writing an entire file is
// good enough for me 99% of the time.
class Test
{
	string readFile(String filename) {
		return File.ReadAllText(filename, Encoding.UTF8);
	}
	
	void writeFile(String filename, string data) {
		File.WriteAllText(filename, data, Encoding.UTF8);
	}
}
```

### Generating Random Numbers

```cs
using System;

class Test
{
	static void Main() {
		// Create a random object
		var random = new Random();
		
		// Create random integer
		int i = random.Next();
		
		// Create random integer from [0, 10)
		int j = random.Next(10);
		
		// Create random boolean
		bool b = random.NextBoolean();
		
		// Create random double on [0, 1)
		double d = random.nextDouble();
	}
}
```