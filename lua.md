# Lua

## Necessary Information

Lua is a light-weight interpreted language.

## General

```lua
-- Function says hello
function sayHello()
	print("Hello, World!")
	
	-- Without local, it will be global
	local x = 3
	
	if x > 0
		x = 5
	elseif x < 0
		x = -5
	else
		x = 0
	end
	
	for i = 1, 100 do
		-- Lua doesn't have +=
		x = x + 1
	end
	
	while x > 0
		x = x - 1
	end
end
```

## Types

### Built-in Types

```lua
-- Number
x = 3
assert(type(x) == "number")

x = 3.0
assert(type(x) == "number")

-- Boolean
b = true
assert(type(b) == "boolean")

-- Arrays are tables
t = {1, 2}
assert(type(t) == "table")

-- Tables as arrays are 1-based
assert(t[1] == 1)

-- Dictionaries are tables
t = {x = 1, y = 2}
assert(type(t) == "table")

```

### Meta-tables

```lua
data = {x=1.0, y=1.0, z=1.0}

setmetatable({
	-- Called when indexing this table
	__index = function(self, idx)
	
	end,
	
	-- Operator overloading
	__add = function(self, rhs)
		-- Do something
	end
	
	__mul = function(self, rhs)
		-- Do something else
	end
})
```

## Common Tasks

### Type Casting

```lua
-- Create number
x = 127

-- Convert to string
s = tostring(x)

-- Convert back to number
y = tonumber(s)

assert(x == y)
```

### Table Manipulation

```lua
-- Create table
t = {3, 1, 2}

-- Get length of table
l = #t

-- Append to table
t[#t + 1] = 0

-- Sort table
table.sort(t)
```

### String Manipulation

```lua
-- Create a string
s1 = "hi there"

-- Create a table
t = { "hi", "there" }

-- Join table
s2 = table.concat(t, " ")

assert(s1 == s2)
```

### Variable arguments

```lua
-- Define a function with variable arguments
function printIntegers(...)
	-- Iterate over the arguments
	for i, v in ipairs(arg) do
		-- And print each one 
		print(v)
	end
end
```

### Generating Random Numbers

```lua
-- Random float from [0, 1)
i = math.random()

-- Random integer from [0, 8)
x = math.floor(math.random() * 8)
```
