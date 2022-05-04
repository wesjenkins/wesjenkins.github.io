# Ruby

## Necessary Information

Ruby is an interpreted multi-paradigm (Mostly OOP) language.

## General

```ruby
def say_hello(x, y)
	puts "Hello, World!"
	
	x = 3
	
	if x > 0
		x = 5
		
	elsif x < 0
		x = -5
		
	else
		x = 0
	end
	
	for i in 0...100
		x += 1
	end
	
	while x > 0
		x -= 1
	end
	
	x += 1 while x < 0
end
```

## Types

### Built-in Types

```ruby
# Integers
x = 3

raise RuntimeError unless x.is_a? Integer

# Float
x = 1.0

raise RuntimeError unless x.is_a? Float

# Booleans
b = true
b = false

# Arrays
xs = [3, 2]
xs[0] = 1
xs.push 3

raise RuntimeError unless x.is_a? Array
```

### Classes

```ruby
# Declaring a class
class Vector
	# Create accessors
	attr_accessor :x
	attr_accessor :y
	attr_accessor :z
	
	# Constructor
	def initialize(x, y, z)
		@x = x
		@y = y
		@z = z
	end
	
	# Overload string conversion
	def to_s
		"(#{@x}, #{@y}, #{@z})"
	end
	
	# Operator overloading
	def +(rhs)
		Vector.new(@x + rhs.x, @y + rhs.y, @z + rhs.z)
	end
	
	def *(rhs)
		@x * rhs.x + @y * rhs.y + @z * rhs.z
	end
end
```

## Common Tasks

### Type Casting

```ruby
# To string
s1 = 5.to_s
s2 = 1.0.to_s
s3 = [1, 2].so_s

# And conversions back
i = s1.to_i
f = s2.to_f
# l = s3.to_a # This one doesn't work

# Conversions between numeric types
i = f.to_i
f = i.to_f
```

### List Manipulation

```python
xs = [1, 2, 3, 4]

# Create a new sorted list
ys = xs.sort

# Sort in place
xs.sort!

raise RuntimeError unless xs == ys

# Reverse out-of- and in-place
xs.reverse
xs.reverse!
```

### String Manipulation

```ruby
# Create a string
s1 = "hi there"

# Split string
xs = s1.split " "

# Join string
s2 = xs.join " "

raise RuntimeError unless s1 == s2
```

### File IO

```ruby
# Open a file for reading and automatically close it with with
data1 = ""
File.open("in.txt", "r") do |f|
	# Read data
	data = f.read
end

# Or just do this one-liner
data2 = File.read "in.txt"

raise RuntimeError unless data1 == data2

# Open a file for writing and automatically close it with with
File.open("out.txt", "w") do |f|
	f.write(data1)
end
```

### Variable arguments

```ruby
# Declare a function accepting any number of arguments
# The arguments can be of any type
def printValues(*vals)
	# vals is going to be an array
	raise RuntimeError unless vals.is_a? Array
	
	# Iterate over the array
	# and print each argument
	vals.each { |val| puts val }
end

# Call just like a normal function
printValues(1, 2)
printValues(3, 1.0)

# Create an array
arr = [1, 2, 3]

# Expand the array as separate arguments
printValues(*arr, 4)
# Note that this is possible for any function
# even ones that are not variable argument
```

### Generating Random Numbers

```ruby
# Random integer from [0, 5]
x = rand 0..5

# Random float from [0, 1)
y = rand
```