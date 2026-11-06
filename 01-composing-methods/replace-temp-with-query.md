# Replace Temp with Query

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace a temporary variable holding a calculation with a method that returns the calculation.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money calculateTotal() {
    Money subtotal = quantity.multiply(unitPrice);
    Money tax = subtotal.multiply(taxRate);
    return subtotal.add(tax);
}
```

## After: refactored code

```java
Money calculateTotal() {
    return subtotal().add(tax());
}

private Money subtotal() {
    return quantity.multiply(unitPrice);
}

private Money tax() {
    return subtotal().multiply(taxRate);
}
```

## Why the refactoring helps

Pulls calculations into named queries so multiple methods can reuse them and the main method becomes declarative.

## When to use it

When a temporary is a reusable derived value and the query is deterministic.

## Cautions

A query may recalculate its value. Avoid this for expensive, time-sensitive, or side-effecting expressions without considering caching.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Convert a calculated discount amount into a query method and use it in two callers.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
