# Replace Magic Number with Symbolic Constant

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace unexplained numeric or string literals with named constants.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
if (retryCount > 3) {
    delay(5000);
}
```

## After: refactored code

```java
private static final int MAX_RETRIES = 3;
private static final Duration RETRY_DELAY = Duration.ofSeconds(5);

if (retryCount > MAX_RETRIES) {
    delay(RETRY_DELAY);
}
```

## Why the refactoring helps

Names the meaning and unit of a literal, reducing accidental inconsistency.

## When to use it

When a literal represents a business rule, threshold, unit, or repeated value.

## Cautions

Do not create constants for obvious values whose meaning is already clear (for example, loop index 0).

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Name timeout, retry, and eligibility thresholds in a service.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
