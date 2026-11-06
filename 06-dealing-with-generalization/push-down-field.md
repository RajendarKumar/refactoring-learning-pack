# Push Down Field

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move a field from a superclass into only the subclasses that use it.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
abstract class Employee { protected String salesTerritory; }
class Engineer extends Employee {}
class Salesperson extends Employee {}
```

## After: refactored code

```java
abstract class Employee {}
class Engineer extends Employee {}
class Salesperson extends Employee {
    private String salesTerritory;
}
```

## Why the refactoring helps

Keeps subclass-specific data out of unrelated objects and clarifies the model.

## When to use it

When only one or a subset of subclasses need a superclass field.

## Cautions

Check persistence mapping, serialization, and code using the superclass type.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Push commissionRate from Employee down to Salesperson.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
