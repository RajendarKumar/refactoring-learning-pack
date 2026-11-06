# Replace Exception with Test

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Check a predictable condition before performing an operation instead of using exceptions for normal control flow.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
try {
    return accounts.get(accountId);
} catch (NoSuchElementException ex) {
    return defaultAccount;
}
```

## After: refactored code

```java
if (!accounts.containsKey(accountId)) {
    return defaultAccount;
}
return accounts.get(accountId);
```

## Why the refactoring helps

Expresses an expected alternative as a normal condition rather than exception handling.

## When to use it

When the exceptional condition is common, predictable, and can be checked cheaply.

## Cautions

A check-then-act sequence can race in concurrent systems. Prefer atomic APIs such as Map.getOrDefault where available.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace a common parse exception with a precheck or a safe parsing API, while considering races.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
