# C

## Necessary Information

C is a compiled "systems" language.

## General

```c
// Preprocessor include of stdio header
#include <stdio.h>

// Main function is the program's entry point
// Must return int, and accept either (void) or (int, char**)
int main(void) {
	printf("Hello, World!\n");
	
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
	
	// Returning 0 means exiting normally
	return 0;
}
```

## Types

### Built-in Types

```c
#include <assert.h>

int main(void) {
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
	
	// Booleans are just 0 = false, 1 = true
	char b = 1;
	
	// Pointer to an integer
	int* p = &x;
	
	// Static array of integers
	int xs[3] = { 1, 2, 3 };
	int ys[]  = { 4, 5, 6 };
	
	return 0;
}
```

### Using Structs

```c
typedef struct {
	int x;
	int y;
	int z;
	
} vec;

int main(void) {
	// Standard initialization
	vec my_vec = { 1, 2, 3 };
	// Follows the order from the declaration
	
	// Designated initializer
	vec your_vec = { .x = 1, .y = 2, .z = 3 };
	// Allows writing fields out of order

	// Changing a struct field
	your_vec.x = 3;
	
	// Take a pointer to a struct object
	vec* vec_p = &my_vec;
	
	// Use -> to access fields from a struct pointer
	vec_p->y = 7; 
	
	return 0;
}

```

## Common Tasks

### Type casting

```
#include <assert.h>

int main(void) {
	// Create an integer
	int x = 3;
	
	// Cast to float
	float y = (float)x;
	
	// Cast back to int
	int x2 = (int)y;
	
	assert(x == x2);
	// Of course, not true for all integers
	
	// Widening conversions are implicit
	long lx = x;
	double d = y;
	
	// And all pointers implicitly cast to void*
	void* p = &y;
	
	return 0;
}
```

### Memory management

```c
int main(void) {
	// Allocate an "array" of 8 integers
	int* array = (int*)malloc(8 * sizeof *array);
	
	// And deallocate it
	free(array);
	
	return 0;
}
```

### String Manipulation

```c
#include <assert.h>
#include <string.h>

int main(void) {
	// Strings are null-terminated
	// Create string
	char* s1 = "hello";
	
	// Create a new array as long as s1
	char* s2 = (char*)malloc(strlen(s1));
	
	// Copy s1 to s2
	strcpy(s2, s1);
	
	// Compare two strings
	assert(!strcmp(s1, s2));
	// (value > 0) means s1 > s2
	// (value < 0) means s1 < s2
	// (value = 0) means s1 == s2
	
	return 0;
}
```

### File IO

```c
// Read an entire file into a buffer
// by trying to first determine its size
char* read_file(char* filename) {
	// Open a file in "binary" mode for reading
	// (Binary only means anything on Windows)
	FILE* fp = fopen(filename, "rb");
	
	// Seek to the end of the file
	fseek(fp, 0, SEEK_END);
	// (0 is the offset from SEEK_END, so it's the exact end)
	
	// Get the current file position,
	// which should be the size of the file
	size_t size = ftell(fp);
	
	// And allocate a buffer to hold it
	char* buff = (char*)malloc(size);
	
	// Then reset the file to the very beginning
	rewind(fp);
	// Or: fseek(fp, 0, SEEK_SET);
	
	// Then read that number of bytes from the file
	fread(buff, 1, size, fp);
	// Remember, args to fread are:
	// (buffer, element size, element count, file pointer)
	
	// Close the file
	fclose(fp);
	// Remember to close files!
	
	// Return buffer, but remember to eventually free it
	return buff;
}

void write_file(char* filename, char* buff, size_t size) {
	// Open a file in "binary" mode for writing
	// (Binary only means anything on Windows)
	FILE* fp = fopen(filename, "wb");
	
	// Then write to that file
	fwrite(buff, 1, size, fp);
	// Remember, args to fwrite are:
	// (buffer, element size, element count, file pointer)
	
	// Close the file
	fclose(filename);
	// Remember to close files!
}

```

### Variable arguments

```c
#include <stdio.h>
#include <stdarg.h>

// This declares a function with variable arguments
// They must have at least one normal argument
void printIntegers(int num, ...) {
	// Set up the object for reading variable arguments
	va_list valist; 
	va_start(valist, num);
	
	
	for (int i = 0; i < num; ++i) {
		// Read the next argument
		// assuming it is an integer
		int arg = va_arg(valist, int);
		// If it isn't an integer?
		// Undefined behavior, could explode maybe.
		
		printf("%d\n", arg);
	}
	
	// Clean up the variable argument object
	va_end(valist):
	// Don't forget to clean up!
}

int main(void) {
	// Call variable argument function
	printIntegers(3, 0, 1, 2);
	// They're called the same way as any other
	
	return 0;
}
```

### Generating Random Numbers

```c
#include <time.h>
#include <stdlib.h>

int main(void) {
	// Common way of seeding random number generator
	// Seeds using the current time
	// Not secure of course, but simple and usually enough
	srand(time(NULL));
	
	// Generates an integer from [0, RAND_MAX]
	int x = rand(); 
	
	// Generates an integer from [0, 7)
	int i = rand() % 7; 
	// HOWEVER, do note that when RAND_MAX % 7 != 0, this is *not* a uniform generator
	// it will ever so slightly favor smaller numbers.
	// Usually, this isn't important, but it's important to remember when generating a lot of numbers.
	
	// Random float from [0, 1)
	float f = (float)rand() / RAND_MAX;
	// Also, note that this doesn't have fantastic properties either
	// The conversion from a 32-bit int to a 32-bit float isn't great
	// Using a double would be better
}
```