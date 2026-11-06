# Add Parameter

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Add a parameter when a method needs additional information to do its job.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money priceFor(Product product) {
    return product.basePrice();
}
```

## After: refactored code

```java
Money priceFor(Product product, CustomerTier tier) {
    return product.basePrice().multiply(tier.priceFactor());
}
```

## Why the refactoring helps

Makes a new dependency explicit instead of reading hidden state.

## When to use it

When the method genuinely needs new caller-provided information.

## Cautions

Update callers deliberately; consider a parameter object if the argument list becomes long.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Add a currency parameter to a formatter that must format in the caller-selected currency.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
