# Rename Method

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Choose a method name that communicates its purpose and behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
boolean check(String supplierId) {
    return repository.existsById(supplierId);
}
```

## After: refactored code

```java
boolean supplierExists(String supplierId) {
    return repository.existsById(supplierId);
}
```

## Why the refactoring helps

Improves discoverability and reduces the need to inspect implementation details.

## When to use it

When a name is vague, misleading, too generic, or no longer matches behaviour.

## Cautions

Use IDE rename refactoring and check external callers, serialized names, and framework conventions.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Rename process() to submitSupplierApplication() and update its callers.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
