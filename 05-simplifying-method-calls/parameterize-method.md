# Parameterize Method

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace similar methods with one method that accepts the varying value as a parameter.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money fivePercentDiscount(Money amount) { return amount.multiply(0.95); }
Money tenPercentDiscount(Money amount) { return amount.multiply(0.90); }
```

## After: refactored code

```java
Money discounted(Money amount, BigDecimal factor) {
    return amount.multiply(factor);
}
```

## Why the refactoring helps

Reduces duplicated algorithms while making the variable part explicit.

## When to use it

When methods perform the same steps and differ only by a value.

## Cautions

If the variants have different business meaning or likely to evolve separately, separate methods may be clearer.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Combine two nearly identical fee methods by passing the fee rate.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
