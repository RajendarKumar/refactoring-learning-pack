# Inline Temp

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Remove a temporary variable that merely stores a simple expression used once.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
double basePrice = quantity * unitPrice;
return basePrice > 1_000 ? basePrice * 0.9 : basePrice;
```

## After: refactored code

```java
return quantity * unitPrice > 1_000
        ? quantity * unitPrice * 0.9
        : quantity * unitPrice;
```

## Why the refactoring helps

Reduces unnecessary local state when the variable does not clarify the code.

## When to use it

When the temporary variable is used once and its expression is easy to understand.

## Cautions

Keep the variable when it improves readability, prevents repeated expensive work, or helps debugging.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Inline a one-use temporary in a small calculation, then compare readability.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
