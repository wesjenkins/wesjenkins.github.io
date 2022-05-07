# Julia Packages

A collection of popular packages and how to use them.

## Plots

### Basic Plotting

```julia
using Plots

# Create a function
f1(x) = 3x + 7
f2(x) = 2x^2 + 3x + 7


# Create x and y data using vectorization
xs = range(0, 10, length=512)
ys1 = f1.(xs)
ys2 = f2.(xs)

# Create plot with no data
plot(title="My Plot", xlabel="My X Label", ylabel="My Y Label")
# (Note, this data can be added during any plot! call too)

# Add data using (!)
plot!(xs, ys, label="Linear")
plot!(xs, ys2, label="Quadratic")

# Display graph
display(plot!())

# Save graph
savefig("graph.png")
```