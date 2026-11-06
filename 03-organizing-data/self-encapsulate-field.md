# Self Encapsulate Field

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Access a field through getter/setter methods even from within the same class.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Employee {
    private BigDecimal salary;
    BigDecimal annualCost() { return salary.multiply(BigDecimal.valueOf(12)); }
}
```

## After: refactored code

```java
class Employee {
    private BigDecimal salary;
    BigDecimal salary() { return salary; }
    BigDecimal annualCost() { return salary().multiply(BigDecimal.valueOf(12)); }
}
```

## Why the refactoring helps

Creates one access point for a field, useful when subclasses or later rules need to intercept access.

## When to use it

When direct field access makes future validation, lazy loading, or overrides difficult.

## Cautions

Do not add boilerplate getters solely for ceremony. In Java, use encapsulation where it protects a real invariant.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Route all reads of an account balance through a named accessor.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
