# Consolidate Duplicate Conditional Fragments

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move identical code that appears in all branches outside the conditional.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
if (isExpress) {
    total = subtotal.add(expressFee);
    audit(order);
} else {
    total = subtotal.add(standardFee);
    audit(order);
}
```

## After: refactored code

```java
if (isExpress) {
    total = subtotal.add(expressFee);
} else {
    total = subtotal.add(standardFee);
}
audit(order);
```

## Why the refactoring helps

Removes duplication and makes the truly conditional part easier to see.

## When to use it

When the same statement or block appears in every branch.

## Cautions

Ensure the moved code has the same execution count and ordering relative to branch-specific work.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Find duplicated audit or metrics calls across if/else branches and consolidate safely.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
