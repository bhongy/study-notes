# API Design Notes

Notes about public interface design, naming. Mostly classes for now.

`.toJSON()` method on class to return data representation of the class instance (rather than only pass the entire class around). Create a new object each call because it's meant to be immutable (caller cannot mutate instance data outside the public interface) <- must make sure not to pass reference to original object through properties from `.toJSON`.

```typescript
// https://medium.com/@ezequiel/immutability-and-builders-with-typescript-b69a51c94e8c
class Person {
  name: string;
  address: { street: string, city: string };

  toJSON() {
    name: this.name,
    address: { ...this.address },
  }
}
```

`.fromJSON(json)` can be defined as a factory method to create a new instance using json data that has structure matched the expected input.

`.toString()` method to define how we want the string representation of the class to look like. Many native method will call `.toString()` on object being passed (implicit coercion).

TBD: `.toUniqueIdentifier` ... a string representation that's unique to the instance.