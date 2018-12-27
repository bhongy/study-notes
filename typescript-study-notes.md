## Good Resources

- https://github.com/gcanti
- https://blog.mariusschulz.com/
- [Official Typescript Doc Site](https://www.typescriptlang.org/docs/home.html)
- https://basarat.gitbooks.io/typescript/content/

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
- `ReadonlyArray<T>` is built-in
- `v is T` annotate returned type for user defined type guard - see notes below
- `v as T` force type casting - better avoid
- [utility types](https://github.com/Microsoft/TypeScript/blob/71286e3d49c10e0e99faac360a6bbd40f12db7b6/src/lib/es5.d.ts#L1391-L1459)
  - also see examples: [Advanced Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html) - section "Predefined conditional types"
- `{ [P in K]: T[P] }` mapped types (iterate through `K` union string literal type) and `T[P]` is the type of the value of property `P`
- `T extends U ? X : Y` conditional type
- `interface T extends A, B, C` extends from multiple interfaces (only interface, class does not support multiple `extends` - i.e. inheritance)

(from https://codeburst.io/five-tips-i-wish-i-knew-when-i-started-with-typescript-c9e8609029db)
- `type Partial<T> = { [P in keyof T]?: T[P]; };` - make all properties optional, already exists in typescript
- `type Readonly<T> = { readonly [P in keyof T]: T[P]; };` - already exists in typescript
- `type Dictionary<T> = Partial<{ [key: string]: Readonly<T> }>;` - all props are readonly + lookup might return `undefined` + optional

- `export =` is like commonjs `module.exports =` must use with `import <var> = require(...)`


## Working with Classes

- assigning a property to an instance if it's not in class definition is not allowed (safe)
- no nominal typing in typescript so if you type that something accepts an instance of class `Foo` it will accepts instances or objects that matches the same structure as `Foo`
  - although `if (v instanceof Foo) { ... }` can be used (like in Flow) to refine the type to a specific class
- `this` can be used as the returned type of a class method `getById(id: string): this`
- be mindful of static vs instance methods `implements` checks instance methods
  - constructor (`new()` signature) is on the static side
- two classes with the same **private** property type (e.g. `private name: string;`) will not typecheck which means this makes the classes nominal
- `private` is only visible inside the current class (not even in subclasses)
- `protected` is visible the current class and its subclasses
  - `protected constructor` signifies this class meant to be inherited and not used directly
- `constructor(readonly name: string) { ... }`: constructor is the only function/method that supports `readonly` in parameter. This is a short-hand for assigning the input to `this[propertyname]`. I'd stick to the standard JS-style (explicit) to avoid using the extra API surface area that is not really needed
- `abstract` keyword can be used to implement an abstract class if you don't intent to instantiate it directly but have other classes derive from it
- an interface can extends a class like `interface A extends MyClass`
- generic classes are only generic over their instance side (not the static side) i.e. static members cannot use the class' type parameter


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

 - [X] Basic Types
 - [X] Variable Declarations
 - [X] Interfaces
 - [X] Classes
 - [X] Functions
 - [X] Generics
 - [ ] Enums
 - [ ] Type Inference
 - [ ] Type Compatibility
 - [X] Advanced Types --- read again
 - [X] Symbols
 - [ ] Iterators and Generators
 - [X] Modules
 - [X] Namespaces
 - [X] Namespaces and Modules
 - [ ] Module Resolution
 - [ ] Declaration Merging


## Other Notes

- always use `strictNullChecks` otherwise it's so permissive and dangerous
- optional property `{ foo?: string }` does not accept `null` like `{ foo: null }`
- `?` only is for "optional" object property or function arguments - unlike Flow it doesn't support as a shorthand of `void | null | T` (I think this is good) so you cannot do `{ foo?: ?string }`
  - optional in typescript basically `| undefined`
  - absence of a property is treat the same as the property has value of `undefined`
- `Object` type (note capital "O" - different than the `object` type) is like `any` (allowing assigning any value types) but will fail any method calls (even ones that exists on the current value)
- `object` type is anything non-primitive
- excess property check is only triggered when an object literal created and pass in function application directly (rather than passing its reference)
- `&` of two objects the type of each keys will be `&` like `string & number` which will not typecheck
- `void` accepts `null` or `undefined` unlike Flow (`void` is type of `undefined`)
  - in typescript type of `undefined` is `undefined` and type of `null` is `null`
  - I'd say don't use `void` and opt for `undefined` (most cases) or `null` explicitly (generally `null` is used as "empty" while `undefined` is used as "not existed")
- using `typeof` as a type guard works for number, string, boolean, symbol
- `instanceof` can be used as a type guard for class instance
- interesting utils

```typescript
type T0 = Exclude<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "b" | "d"
type T1 = Extract<"a" | "b" | "c" | "d", "a" | "c" | "f">;  // "a" | "c"
// note extracts only "Function" type
type T03 = Extract<string | number | (() => void), Function>;  // () => void

type FunctionPropertyNames<T> = { [K in keyof T]: T[K] extends Function ? K : never }[keyof T];
type FunctionProperties<T> = Pick<T, FunctionPropertyNames<T>>;
type NonFunctionPropertyNames<T> = { [K in keyof T]: T[K] extends Function ? never : K }[keyof T];
type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;

interface Part {
    id: number;
    name: string;
    subparts: Part[];
    updatePart(newName: string): void;
}

type T40 = FunctionPropertyNames<Part>;  // "updatePart"
type T41 = NonFunctionPropertyNames<Part>;  // "id" | "name" | "subparts"
type T42 = FunctionProperties<Part>;  // { updatePart(newName: string): void }
type T43 = NonFunctionProperties<Part>;  // { id: number, name: string, subparts: Part[] }

type Omit<T, K> = Pick<T, Exclude<keyof T, K>>;
```
from: https://www.typescriptlang.org/docs/handbook/advanced-types.html


## Why do I like Typescript?

- community! libdefs are very very well typed and a lot of great articles from people in the community.
- no confusing "nullable" syntax like `?T` - `?` is for optional
- object type inference is straight forward

```typescript
const one = { a: 1, b: 2 };
const two = { c: 3, d: 4 };
const three = { ...one, ...two };
// typeof three => { a: number, b: number, c: number, d: number }
const { a, ...four } = one;
// typeof four => { b: number }
```
- index type query and indexed access is powerful for expressing type contraints
  - https://www.typescriptlang.org/docs/handbook/advanced-types.html
- function overloads
- works really well with VSCode