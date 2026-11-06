# Change Reference to Value

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace a shared mutable reference with an immutable value object when identity is unnecessary.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Coordinates {
    double latitude;
    double longitude;
}

Coordinates a = sharedCoordinates;
Coordinates b = a;
b.latitude = 10; // silently changes a as well
```

## After: refactored code

```java
record Coordinates(double latitude, double longitude) {}

Coordinates a = new Coordinates(12.9, 77.6);
Coordinates b = new Coordinates(10.0, 20.0); // independent immutable value
```

## Why the refactoring helps

Eliminates shared mutable state and makes equality based on value.

## When to use it

When objects are small, immutable, and have no meaningful identity.

## Cautions

If callers rely on shared mutation or object identity, changing to value semantics can break behaviour.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Convert a mutable Money or Coordinate class into an immutable record.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
