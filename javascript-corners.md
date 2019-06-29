Detail about Javascript that I generally forget. Mostly class stuff.

# Classes

`super` refers to the parent constructor.

You can delegate to the parent class's method by doing `super.<method>`. For example, a method `eat` is override in the subclass like `eat(food) { super.eat(food); this.hungry = false; }`

You can't use `this` in constructor until after you call `super`.
https://overreacted.io/why-do-we-write-super-props/

# Functions

`fn.apply(null, arguments)` when seeing that think `fn(...args)`