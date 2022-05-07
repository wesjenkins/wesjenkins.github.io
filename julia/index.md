# Python

## Necessary Information

Python is an interpreted multi-paradigm language.

## General

```julia
function sayHello(x, y)
	# Print
	println("Hello, World!")
	
	x = 3
	
	if x > 0
		x = 5
	elseif x < 0
		x = -5
	else
		x = 0
	end
	
	for i in 0:100
		x += 1
	end
	
	while x > 0
		x -= 1
	end
end
```

## Types

### Built-in Types

```julia
# Integer
x = 3

@assert typeof(x) <: Integer

# Float
x = 3.0

@assert typeof(x) <: AbstractFloat

# Tuples are not mutable
x = (1, 2)
@assert typeof(x) <: Tuple{<:Integer, <:Integer}
# x[0] = 3 # Doesn't work

# Arrays are mutable
x = [1, 2]
@assert typeof(x) <: Vector{<:Integer}
x[0] = 1 # Does work
```

### Structs

```julia
# Structs are immutable by default!
struct Vec
	x
	y
	z
end

# Overload methods using multiple dispatch
function Base.:+(lhs :: Vec, rhs :: Vec)
	Vec(lhs.x + rhs.x, lhs.y + rhs.y, lhs.z + rhs.z)
end

function Base.:*(lhs :: Vec, rhs :: Vec)
	lhs.x * rhs.x + lhs.y * rhs.y + lhs.z * rhs.z
end

v1 = Vec(1, 2, 3)
v2 = Vec(4, 5, 6)
v3 = v1 + v2

d = v1 * v3
```

## Common Tasks

### Type Casting

```julia
# Conversions to string
s1 = string(5)
s2 = string(1.0)
s3 = string([1, 2])
s4 = string((1, 2))

# And conversions back
i = parse(Int, s1)
f = parse(Float64, s2)

# Conversions between numeric types
f = Float64(i)
i = round(Int, f)
# Cannot simply cast from Float to Int, or you'll get an exception
```

### Array Manipulation

```julia
# Create an array
xs = [4, 1, 2, 3]

# Form into matrix
mat = hcat(xs, [5, 6, 7, 8])

# Create a new sorted array
ys = sort(xs)

# Sort in place
sort!(xs)

@assert xs == ys

# Does what you expect
reverse(xs)
reverse!(xs)
```

### String Manipulation

```julia
# Create a string
s1 = "hi there"

# Split string
xs = split(xs, " ")

# Join string
s2 = join(xs, " ")

@assert s1 == s2
```

### File IO

```julia
# Open a file and automatically close it
open("textfile.txt", "r") do io
	# Read text
	text = read(io, String)
end

# Open a file and automatically close it
open("out.txt", "w") do io
	# write text
	text = write(io, text)
end
```

### Variable arguments

```julia
# Declare a function accepting any number of arguments
# The arguments can be of any type
function printValues(vals...)
	# Iterate over the tuple
	for val in vals
		# And print each argument
		println(val)
	end
end

# Call just like a normal function
printValues(1, 2)
printValues(3, 4, 5)

# Create a tuple
tup = (1, 2, 3)

# Expand the tuple as separate arguments
printValues(tup..., 4)
# Note that this is possible for any function
# even ones that are not variable argument
```

### Generating Random Numbers

```python
# Random integer from [0, 5]
x = rand(0:5)

# Random double from [0, 1)
y = rand()

# Random choice
z = rand([1, 5, 7])

# 3x3 matrix of values on [0, 1)
xs = rand(3, 3)
```