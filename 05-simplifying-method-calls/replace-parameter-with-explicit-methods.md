# Replace Parameter with Explicit Methods

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace a boolean or mode parameter with separate methods whose names express the alternatives.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Report generate(boolean includeHistory) { ... }
```

## After: refactored code

```java
Report generateCurrentReport() { ... }
Report generateReportWithHistory() { ... }
```

## Why the refactoring helps

Call sites become self-explanatory and invalid combinations become harder to express.

## When to use it

When a parameter selects between two or a few distinct behaviours.

## Cautions

For many combinations or frequently changing policies, consider Strategy or a parameter object instead.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace send(notification, true) with sendUrgentNotification() and sendStandardNotification().

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
