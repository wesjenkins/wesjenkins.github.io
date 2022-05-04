# Java

## Necessary Information

Java is a popular compiled/interpreted language.

## General

```java
// Everything must live inside a class
public class Main
{
	// Main function
	public static void main(String[] args) {
		// Print hello
		System.out.println("Hello, World!");
		
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
	}
}
```

## Types

### Built-in Types

```java
public class Main {
	public static void main(String[] args) {
		// Integers and longs
		int x = 1;
		Integer x_box = new Integer(x);
		
		assert x == x_box.intValue();
		
		long w = 13;
		Long w_box = new Long(w);
		
		assert w == w_box.longValue();
		
		// Floats and doubles
		float y = 1.0f;
		Float y_box = new Float(y);
		
		assert y == y_box.floatValue();
		
		double z = 1.0;
		Double z_box = new Double(z);
		
		assert z == z_box.doubleValue();
		
		// Strings
		String s = "Hi!";
		
		// Arrays
		int[] xs = { 1, 2, 3, 4 };
	}
}
```

### Classes

```java
// Due to dumb file requirements, make this non-public
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
	
	public override toString() {
		return String.format("(%d, %d, %d)", x, y, z);
	}
	
	// No fancy operator overloading
	public Vector add(Vector rhs) {
		return new Vector(x + rhs.x, y + rhs.y, z + rhs.z);
	}
	
	public int dot(Vector rhs) {
		return x * rhs.x + y * rhs.y + z * rhs.z;
	}
}

public class Main
{
	public static void main(String[] args) {
		// Create objects
		Vector v1 = new Vector(1, 2, 3);
		Vector v2 = new Vector(4, 5, 6);
		
		// Use methods
		Vector v3 = v1.add(v2);
		int dot = v1.dot(v2);
	}
}
```

## Common Tasks

### Type Casting

```java
class Base {}
class Child extends Base {}
class Child2 extends Base {}

public class Main
{
	public static void main(String[] args) {
		// Create an integer
		int x = 3;
		
		// Cast to float
		float y = (float)x;
		
		// Cast back to int
		int x2 = (int)y;
		
		assert x == x2;
		
		// Classes implicitly convert to parent class
		Base base = new Child();
		
		// Cast back to child class dynamically
		Child child = (Child)base;
		
		// This will throw a runtime error
		// Child2 child2 = (Child2)base;
	}
}
```

### List Manipulation

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Main
{
	public static void main(String[] args) {
		// Create an array
		int[] arr = { 1, 2, 3, 4 };
		
		// Use Java 8 Streams to convert to list
		// (A bit overkill, but a good example of how it works)
		List<Integer> list = Arrays.stream(arr)
		                           .boxed()
		                           .collect(Collectors.toList());
		
		// Add a new integer to the end
		list.add(new Integer(5));
	}
}
```

### String Manipulation

```java
public class Main
{
	public static void main(String[] args) {
		// Create a string
		String s = "hello";
		String s2 = " there";
		
		// Add strings together
		String s3 = s + s2;
		
		// Create a substring
		String sub = s3.substring(0, 5);
		
		// String equality
		assert s.equals(sub);
		
		// Substring search
		assert s3.indexOf("there") == 6;
		
		assert s3.indexOf("asdf") == -1;
	}
}
```

### File IO

```java
public class Main
{
	char[] readFile(String filename) {
		FileInputStream fp = null;
		
		try {
			fp = new FileInputStream(filename);
			
			char[] buff = new char[fp.available()];
			
			fp.read(buff):
			
			return buff;
			
		} finally {
			if (fp != null)
				fp.close();
		}
	}
	
	void writeFile(String filename, char[] data) {
		FileOutputStream fp = null;
		
		try {
			fp = new FileOutputStream(filename);
			
			fp.write(data);
			
		} finally {
			if (fp != null)
				fp.close();
		}
	}
}
```

### Generating Random Numbers

```java
public class Main
{
	public static void main(String[] args) {
		// Create random object seeded with time
		Random random = new Random(System.currentTimeMillis());
		
		// Create random integer
		int i = random.nextInt();
		
		// Create random integer from [0, 10)
		int j = random.nextInt(10);
		
		// Create random boolean
		bool b = random.nextBool();
		
		// Create random float on [0, 1)
		float f = random.nextFloat();
		
		// Create random double on [0, 1)
		double d = random.nextDouble();
	}
}
```