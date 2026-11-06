# Extract Variable

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Give a meaningful name to a complex expression.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
if (order.total() > 0 && order.total() > customer.creditLimit() - customer.balance()) {
    reject(order);
}
```

## After: refactored code

```java
Money availableCredit = customer.creditLimit().subtract(customer.balance());
boolean exceedsAvailableCredit = order.total().isGreaterThan(availableCredit);

if (order.total().isPositive() && exceedsAvailableCredit) {
    reject(order);
}
```

## Why the refactoring helps

Names the business meaning of an expression and makes the condition easier to review.

## When to use it

When an expression is long, repeated, or represents a business concept.

## Cautions

Choose a name that explains meaning, not merely the mechanics of the expression.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract the expression that checks whether a supplier is eligible for onboarding.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
