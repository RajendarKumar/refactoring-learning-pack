# Extract Interface

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Define a smaller interface containing the operations clients need from a class.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class SupplierRepository {
    Supplier findById(String id) { ... }
    void save(Supplier supplier) { ... }
    void rebuildSearchIndex() { ... }
}
```

## After: refactored code

```java
interface SupplierReader {
    Supplier findById(String id);
}
class SupplierRepository implements SupplierReader {
    public Supplier findById(String id) { ... }
    void save(Supplier supplier) { ... }
    void rebuildSearchIndex() { ... }
}
```

## Why the refactoring helps

Allows clients to depend on a focused capability rather than a concrete, broad class.

## When to use it

When a class serves multiple roles or consumers need only a subset of its methods.

## Cautions

Keep interfaces purposeful; avoid creating one interface per class without a useful substitution boundary.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract SupplierLookup from a repository used by read-only services.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
