# Remove Parameter

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Remove a parameter that is unused or can be derived from existing information.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money total(Order order, boolean includeTax) {
    return order.totalWithTax();
}
```

## After: refactored code

```java
Money total(Order order) {
    return order.totalWithTax();
}
```

## Why the refactoring helps

Simplifies the API and removes information the method does not need.

## When to use it

When the parameter is unused, redundant, or always has the same value.

## Cautions

Check overloads, reflection, frameworks, and public API compatibility before removing it.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove a redundant locale parameter when the formatter already owns a configured locale.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
