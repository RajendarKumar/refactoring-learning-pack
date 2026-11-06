# Code Smell: Dead Code

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A variable, parameter, field, method, class, or branch is no longer used or reachable.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The IDE or static analysis marks code as unused.
- A feature was removed but its helper methods remain.
- Branches are impossible under current invariants.

## Before: a problematic design

```java
class PricingService {
    BigDecimal currentPrice(Product product) {
        return product.basePrice();
    }

    // Old promotion model removed last year; no callers remain.
    BigDecimal calculateLegacyPromotion(Product product) {
        return product.basePrice().multiply(new BigDecimal("0.90"));
    }
}
```

## After: a possible refactoring

```java
class PricingService {
    BigDecimal currentPrice(Product product) {
        return product.basePrice();
    }
}
```

## Why the refactoring helps

Removing obsolete code reduces the surface area readers and maintainers must understand. Version control preserves the historical implementation if it is ever needed for reference.

## Refactorings to consider

- Delete the unused code; use Inline Method or Collapse Hierarchy when removal is part of simplifying a larger structure.

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Before deleting code in frameworks, inspect reflection, dependency injection, serialization, configuration, scheduled jobs, external callers, and public APIs. Tests and static analysis may not reveal every dynamic reference.

## Practice exercise

Use IDE usage analysis and static analysis to identify one candidate. Verify that no runtime or external contract uses it, then remove it and run the full test suite.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Dead Code](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
