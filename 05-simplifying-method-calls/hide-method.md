# Hide Method

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Reduce the visibility of a method that is not part of the class’s public contract.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
public class PricingEngine {
    public BigDecimal calculateInternalTax(BigDecimal amount) { ... }
}
```

## After: refactored code

```java
public class PricingEngine {
    private BigDecimal calculateInternalTax(BigDecimal amount) { ... }
}
```

## Why the refactoring helps

Shrinks the public API and reduces the number of ways other code can depend on the class.

## When to use it

When a method is used only inside its class or package.

## Cautions

Check reflection, dependency injection, serialization, tests, and framework access before narrowing visibility.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Identify public helper methods that should be private or package-private.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
