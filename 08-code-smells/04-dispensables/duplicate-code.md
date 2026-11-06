# Code Smell: Duplicate Code

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

The same or nearly identical logic appears in multiple places, so fixes and rule changes must be repeated.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Two methods have copied validation or transformation steps.
- A bug fix must be applied to several similar blocks.
- The code differs only in a small input or parameter.

## Before: a problematic design

```java
class SupplierService {
    String normalizeName(String name) {
        return name.trim().replaceAll("\s+", " ").toUpperCase(Locale.ROOT);
    }
}
class CustomerService {
    String normalizeName(String name) {
        return name.trim().replaceAll("\s+", " ").toUpperCase(Locale.ROOT);
    }
}
```

## After: a possible refactoring

```java
final class NameNormalizer {
    private NameNormalizer() {}

    static String normalize(String name) {
        return name.trim().replaceAll("\s+", " ").toUpperCase(Locale.ROOT);
    }
}

class SupplierService {
    String normalizeName(String name) { return NameNormalizer.normalize(name); }
}
class CustomerService {
    String normalizeName(String name) { return NameNormalizer.normalize(name); }
}
```

## Why the refactoring helps

One implementation owns the shared transformation. A correction is made once and all callers receive it.

## Refactorings to consider

- Extract Method
- Pull Up Method
- Form Template Method
- Substitute Algorithm

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Similar-looking code is not always duplicate business logic. If two blocks have different reasons to change, keep them separate or extract only the truly shared mechanism.

## Practice exercise

Find duplicated code in two services. Decide whether it is identical behaviour or merely similar syntax, then extract the shared behaviour with a domain-appropriate name.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Duplicate Code](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
