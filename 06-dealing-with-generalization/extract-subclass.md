# Extract Subclass

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Create a subclass for a subset of objects that need additional fields or behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Employee {
    private boolean onCall;
    private Money onCallAllowance() { ... }
}
```

## After: refactored code

```java
class Employee { /* common employee behaviour */ }
class OnCallEmployee extends Employee {
    private boolean onCall;
    private Money onCallAllowance() { ... }
}
```

## Why the refactoring helps

Keeps specialized state and behaviour out of the general class.

## When to use it

When only some instances require a coherent set of extra features.

## Cautions

Use composition or a role/strategy when the specialization is dynamic or orthogonal to the main type.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract ContractEmployee from Employee when contract-specific rules are substantial.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
