# Extract Superclass

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Create a superclass for common fields and methods shared by multiple classes.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class SupplierAgreement { String id; Instant createdAt; void audit() { ... } }
class CustomerAgreement { String id; Instant createdAt; void audit() { ... } }
```

## After: refactored code

```java
abstract class Agreement {
    protected String id;
    protected Instant createdAt;
    void audit() { ... }
}
class SupplierAgreement extends Agreement {}
class CustomerAgreement extends Agreement {}
```

## Why the refactoring helps

Captures a real shared concept and removes duplicated implementation.

## When to use it

When multiple classes share stable state and behaviour that belong to a common abstraction.

## Cautions

Inheritance creates coupling. If the shared behaviour is incidental, extract a collaborator instead.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract a common AuditableEntity superclass only when lifecycle semantics truly match.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
