# Code Smell: Lazy Class

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A class provides so little behaviour or value that maintaining the extra abstraction costs more than it saves.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The class has one trivial method and no meaningful state.
- It forwards every call without adding policy or hiding a dependency.
- The abstraction was introduced for a future scenario that never arrived.

## Before: a problematic design

```java
class PhoneFormatter {
    String format(String rawNumber) {
        return PhoneNumberLibrary.format(rawNumber);
    }
}

class CustomerProfile {
    private final PhoneFormatter formatter;
    String displayPhone(String raw) { return formatter.format(raw); }
}
```

## After: a possible refactoring

```java
class CustomerProfile {
    String displayPhone(String raw) {
        return PhoneNumberLibrary.format(raw);
    }
}
```

## Why the refactoring helps

The unnecessary wrapper is removed, reducing indirection and the number of classes a maintainer must understand.

## Refactorings to consider

- Inline Class
- Collapse Hierarchy
- Remove Middle Man

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

A small class is not automatically lazy. A one-method adapter, interface, or boundary can be valuable when it isolates a third-party dependency, enables testing, or expresses a domain concept.

## Practice exercise

Find a class that mostly forwards calls. Decide whether it provides a boundary or policy. If not, inline its behaviour and update callers.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Lazy Class](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
