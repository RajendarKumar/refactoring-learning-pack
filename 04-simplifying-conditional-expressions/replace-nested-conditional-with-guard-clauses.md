# Replace Nested Conditional with Guard Clauses

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Handle exceptional or invalid cases first and return early, leaving the main path unindented.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Money payout(Employee employee) {
    if (employee != null) {
        if (employee.isActive()) {
            if (employee.salary() != null) {
                return employee.salary();
            }
        }
    }
    return Money.ZERO;
}
```

## After: refactored code

```java
Money payout(Employee employee) {
    if (employee == null) return Money.ZERO;
    if (!employee.isActive()) return Money.ZERO;
    if (employee.salary() == null) return Money.ZERO;
    return employee.salary();
}
```

## Why the refactoring helps

Emphasizes the happy path and reduces nesting.

## When to use it

When nested conditions mostly handle invalid, exceptional, or boundary cases.

## Cautions

Use clear guard conditions and preserve exact precedence and fallback semantics.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Convert nested supplier eligibility checks into early-return guard clauses.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
