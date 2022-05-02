# Python

## Necessary Information

Python is an interpreted multi-paradigm language.

## General

```python

# Import module
import random

# Function says hello
def sayHello(x, y):
	"""This function says hello"""
		
	print("Hello, World!")
	
	x = 3
	
	if x > 0:
		x = 5
	elif x < 0:
		x = -5
	else:
		x = 0
	
	for i in range(100):
		x += 1
	
	while x > 0:
		x -= 1
```

## Types

### Built-in Types

```python
# Integer
x = 3
assert type(x) == int

# Float
x = 6
assert type(y) == float

# Boolean
x = True
assert type(x) == bool

# Tuples are not mutable
x = (1, 2)
assert type(x) == tuple
# x[0] = 3 # Doesn't work

# Lists are mutable
x = [1, 2]
assert type(x) == list
x[0] = 3 # Does work

```

### Classes

```python
# Declaring a class
class Vec(object):
	# Constructor
	def __init__(self, x, y):
		self.x = x
		self.y = y
	
	# Overload REPL representation
	def __repr__(self):
		return f"Vec({self.x}, {self.y})"
	
	# Overload conversion to string (Like inside print)
	def __str__(self):
		return f"({self.x}, {self.y})"
	
	# Overload operators (Pretty self-exp)
	def __add__(self, rhs):
		return Vec(self.x + rhs.x, self.y + rhs.y)
	
	def __sub__(self, rhs):
		return Vec(self.x - rhs.x, self.y - rhs.y)
	
	def __mul__(self, rhs):
		return x * rhs.x + y * rhs.y

# Import dataclass decorator
from dataclasses import dataclass

# Dataclasses have automatic constructors
@dataclass
class Person:
	name: str
	age: int
```

## Common Tasks

### List Manipulation

```python
xs = [1, 2, 3, 4]

# Create a new sorted list
ys = sorted(xs)

# Sort in place
xs.sort()

assert xs == ys

# Reverse in place
xs.reverse()
```

### String Manipulation

```python
# Create a string
s1 = 'hi there'

# Split string
xs = s1.split(' ')

# Join string
s2 = ' '.join(xs)

assert s1 == s2
```

### Generating Random Numbers

```python

# Import random library
import random

# Random integer from [0, 5]
x = random.randint(0, 5)

# Random float from [0, 1)
y = random.random()

# Random choice
x = random.choice([1, 2])
```
