# Introduce Foreign Method

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Add a small helper in your own code when a library class lacks a method you need and cannot be modified.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
long daysBetween(LocalDate start, LocalDate end) {
    return ChronoUnit.DAYS.between(start, end);
}
```

## After: refactored code

```java
// Utility owned by your application; LocalDate itself remains unchanged.
final class Dates {
    private Dates() {}
    static long businessDaysCalendarSpan(LocalDate start, LocalDate end) {
        return ChronoUnit.DAYS.between(start, end);
    }
}
```

## Why the refactoring helps

Adds the missing convenience without changing or forking a third-party class.

## When to use it

When a library type lacks a small operation needed by your application.

## Cautions

Keep the helper close to its usage and name it to distinguish your application rule from standard library semantics.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Add an application helper for a missing formatting operation on a third-party date type.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
