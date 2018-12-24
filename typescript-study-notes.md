## Good Resources

- https://github.com/gcanti
- https://blog.mariusschulz.com/
- https://basarat.gitbooks.io/typescript/content/
- [Official Typescript Doc Site](https://www.typescriptlang.org/docs/home.html)

## API Reference

- `keyof T` get union string literal from keys of object type `T`
  - `keyof typeof obj` - convert object value to type before calling `keyof`
  - like flow `$Keys`
- `T extends U` generic type constrain 
  - `function fn<T extends string>(in: T) {}`
- `T = U` default generic parameter type
  - `function fn<T = {}>(in: T) {}`
- `readonly propKey: T;` mark a property as read-only (interface, literal, class)
- `Readonly<T>` make all properties (shallow) of `T` read-only
- `v is T` annotate returned type for user defined type guard - see notes below
- `v as T` force type casting - better avoid

(from https://codeburst.io/five-tips-i-wish-i-knew-when-i-started-with-typescript-c9e8609029db)
- `type Partial<T> = { [P in keyof T]?: T[P]; };` - make all properties optional
- `type Readonly<T> = { readonly [P in keyof T]: T[P]; };` - this already exists in typescript
- `type Dictionary<T> = Partial<{ [key: string]: Readonly<T> }>;` - all props are readonly + lookup might return `undefined` + optional


## Working with Classes

- assigning a property to an instance if it's not in class definition is not allowed (safe)
- no nominal typing in typescript so if you type that something accepts an instance of class `Foo` it will accepts instances or objects that matches the same structure as `Foo`
  - although `if (v instanceof Foo) { ... }` can be used (like in Flow) to refine the type to a specific class


## [Typescript Deep-dive @basarat](https://basarat.gitbooks.io/typescript/docs/types/type-system.html)

### Typescript's Type System

- Enums
  - `enum`, `const enum`, `preserveConstEnums`
  - Enum with static functions
- lib.d.ts
  - examples of how to type class that has both static methods and instance methods `new()`
  - `declare global`
- Functions: overloading function declaration
- Callable: note inline callable signature to define overload
- Type Assertion: **unsafe**. force type casting `const foo = {} as Foo;`
- Freshness: note how object literal fail typechecking only when created inline but not when assign to a variable and passing the variable as param
- Type Guard: see Literal Type Guard for using discriminated union
  - user defined type guard `is Foo` instead of just returning a boolean
- Literal Types: good example how to create String based enums
- Type Inference: always use `noImplicitAny` config
- Type Compatibility
  - **Be careful** Typescript does not have nominal typing on like flow does for classes (see section "Structural")
- Discriminated Unions:
  - types must share a property which is a literal value (string, number, boolean)
  - always add exhaustive check `: never` when a function takes discriminated union input to make sure typescript will error when new "types" are added and not handled
- Index Signatures
  - use a limited set of string literals as key: `type T = { [k in 'a' | 'b']?: number }` - generally use with `keyof typeof obj` to get the discriminated union of keys from `obj`
- Moving Types
  - use `import TypeAlias = Namespace.OriginalClass` to alias classes
  - pattern to capture a type of a class property
  - using `const` to declare a variable to a string literal will have the type of the literal string (not generic string type) so we can use `typeof` to get the literal string type
- Exception handling
  - Exceptions should be exceptional - only throw when it's exceptional 
  - Unless you want to handle the error in a very generic (simple / catch-all etc) way, don't throw an error.
- Mixins: good example how to use it to compose functinality to classes
  - `<Constructor = {}>` syntax means default type for the `Constructor` is `{}` https://blog.mariusschulz.com/2017/06/02/typescript-2-3-generic-parameter-defaults#another-example

- [nominal typing](https://basarat.gitbooks.io/typescript/docs/tips/nominalTyping.html). Typescript doesn't have it - the article shows work-arounds. Not sure lacking of nominal typing is a problem until I program more with it (i.e. do you actually care what "name" the class has as long as their interfaces are compatible?). `instanceof` still work to refine the type though.


## [Typescript Official Doc Site](https://www.typescriptlang.org/docs/home.html)

### Handbook
[ ] ...


## Other Notes

- optional property `{ foo?: string }` does not accept `null` like `{ foo: null }`
- `?` only is for "optional" object property or function arguments - unlike Flow it doesn't support as a shorthand of `void | null | T` (I think this is good) so you cannot do `{ foo?: ?string }`
