# Introduce Assertion

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Add an assertion to document and verify an assumption that should always hold at a particular point.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
void applyDiscount(Order order) {
    // Assumption: total is non-negative.
    order.apply(discount);
}
```

## After: refactored code

```java
void applyDiscount(Order order) {
    assert order.total().signum() >= 0 : "Order total must be non-negative";
    order.apply(discount);
}
```

## Why the refactoring helps

Makes an invariant explicit and can catch programming errors close to their source.

## When to use it

When a condition is a programmer assumption rather than ordinary user-input validation.

## Cautions

Java assertions are disabled unless enabled with -ea. Use explicit validation for production input guarantees.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Add assertions for internal invariants in a calculation routine and distinguish them from validation.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
