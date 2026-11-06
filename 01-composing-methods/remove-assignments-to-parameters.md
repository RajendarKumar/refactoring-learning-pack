# Remove Assignments to Parameters

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Avoid changing a method parameter; create a local variable for a transformed value.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money finalPrice(Money price) {
    price = price.multiply(discountFactor);
    return price.add(shippingCost);
}
```

## After: refactored code

```java
Money finalPrice(Money price) {
    Money discountedPrice = price.multiply(discountFactor);
    return discountedPrice.add(shippingCost);
}
```

## Why the refactoring helps

Preserves the caller-provided value and makes data flow easier to follow.

## When to use it

When a parameter is reassigned, especially in code with multiple branches.

## Cautions

In Java, parameters are local variables, but reassigning them can still obscure intent and confuse debugging.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove a parameter reassignment from a method that normalizes a supplier code.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
