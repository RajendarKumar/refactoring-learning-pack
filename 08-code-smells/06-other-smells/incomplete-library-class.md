# Code Smell: Incomplete Library Class

**Category:** Other Smells  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A library type almost meets the application’s needs, but a missing operation forces repeated workarounds in client code.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Several callers implement the same helper around a library type.
- The missing operation is clearly related to the library abstraction.
- You cannot or should not modify the third-party or JDK class itself.

## Before: a problematic design

```java
boolean isBusinessDay(LocalDate date, Set<LocalDate> holidays) {
    boolean weekday = date.getDayOfWeek() != DayOfWeek.SATURDAY
            && date.getDayOfWeek() != DayOfWeek.SUNDAY;
    return weekday && !holidays.contains(date);
}

// Similar implementations are repeated in several services.
```

## After: a possible refactoring

```java
final class BusinessCalendar {
    private final Set<LocalDate> holidays;

    BusinessCalendar(Set<LocalDate> holidays) {
        this.holidays = Set.copyOf(holidays);
    }

    boolean isBusinessDay(LocalDate date) {
        DayOfWeek day = date.getDayOfWeek();
        boolean weekday = day != DayOfWeek.SATURDAY && day != DayOfWeek.SUNDAY;
        return weekday && !holidays.contains(date);
    }
}
```

## Why the refactoring helps

The application-specific operation is added in a local extension/service rather than modifying the library class. All clients share one tested implementation.

## Refactorings to consider

- Introduce Local Extension
- Introduce Foreign Method
- Adapter (when a wrapper also normalizes an external API)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not subclass final or value-like library classes just to add a helper. Prefer composition, a utility with a clear domain name, or a wrapper. Avoid a generic Utils class that becomes a dumping ground.

## Practice exercise

Find a library type for which your code repeats a missing operation. Create a narrow extension service and replace the duplicated call-site logic.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Incomplete Library Class](https://refactoring.guru/refactoring/smells/other)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
