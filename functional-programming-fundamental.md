# Function Programming Fundamental

Everything FP people do is to achieve function composition.

Core concepts:
  - immutability: avoid/limit mutable state
  - pure functions: avoid/limit side-effects
  - higher-order function: any function that _either_ takes a function as input _or_ returns another function.
  - functions are the mean for logic abstraction

Laziness is essential to abstract away lower-level performance concerns for collections (so that concern does not leak in to the declarative programming model in FP). It is essential in Haskell, ReactiveX (e.g. Rxjs), Java Stream. I believe laziness is also core to Haskell currying but I do not know (have to figure that out).

Currying: transforming a function that takes multiple parameters to a series of functions that take one parameter at a time.
Function application: execute/call a function.
Partially applied: "apply" a function with numbers of parameters fewer than what total number of parameters the function expects which returns a partially applied function.