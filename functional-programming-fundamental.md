# Function Programming Fundamental

Everything FP people do is to achieve function composition.

Core concepts:
  - immutability: avoid/limit mutable state
  - pure functions: avoid/limit side-effects
  - higher-order function: any function that _either_ takes a function as input _or_ returns another function.
  - functions are the mean for logic abstraction

Currying: transforming a function that takes multiple arguments to a series of functions that take one argument at a time.
Function application: execute/call a function.
Partially applied: "apply" a function with numbers of arguments fewer than what total number of arguments the function expects which returns a partially applied function.