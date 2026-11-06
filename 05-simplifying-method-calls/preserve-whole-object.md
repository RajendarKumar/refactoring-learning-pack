# Preserve Whole Object

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Pass the object containing needed values rather than extracting and passing several individual values.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
int daysUntilExpiry(Agreement agreement) {
    return calculateDays(agreement.startDate(), agreement.endDate(), agreement.renewalDate());
}
```

## After: refactored code

```java
int daysUntilExpiry(Agreement agreement) {
    return calculateDays(agreement);
}

int calculateDays(Agreement agreement) {
    return calculate(agreement.startDate(), agreement.endDate(), agreement.renewalDate());
}
```

## Why the refactoring helps

Keeps related information together and reduces coupling to the object’s internal field layout.

## When to use it

When multiple fields from one object are always passed together.

## Cautions

Avoid passing huge objects across boundaries where only a small stable contract should be exposed.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace passing supplier name, id, and country separately with a Supplier reference where appropriate.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
