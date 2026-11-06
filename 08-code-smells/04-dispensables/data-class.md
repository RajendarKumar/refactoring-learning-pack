# Code Smell: Data Class

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A class contains fields and accessors but no meaningful behaviour, while other classes manipulate its data in detail.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- All business rules involving the data live in external services.
- Callers repeatedly retrieve several fields and calculate the same result.
- The class exposes mutable collections or setters that let callers break invariants.

## Before: a problematic design

```java
class Customer {
    private CustomerTier tier;
    private int loyaltyPoints;
    public CustomerTier getTier() { return tier; }
    public int getLoyaltyPoints() { return loyaltyPoints; }
}

class DiscountService {
    BigDecimal discountFor(Customer customer) {
        if (customer.getTier() == CustomerTier.GOLD && customer.getLoyaltyPoints() > 1000) {
            return new BigDecimal("0.15");
        }
        return BigDecimal.ZERO;
    }
}
```

## After: a possible refactoring

```java
class Customer {
    private CustomerTier tier;
    private int loyaltyPoints;

    BigDecimal discountRate() {
        if (tier == CustomerTier.GOLD && loyaltyPoints > 1000) {
            return new BigDecimal("0.15");
        }
        return BigDecimal.ZERO;
    }
}

class DiscountService {
    BigDecimal discountFor(Customer customer) {
        return customer.discountRate();
    }
}
```

## Why the refactoring helps

Behaviour that depends on Customer state is located with that state, reducing duplicated knowledge and protecting invariants.

## Refactorings to consider

- Move Method
- Encapsulate Field
- Encapsulate Collection
- Preserve Whole Object

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

DTOs, API request records, persistence projections, and event payloads are often intentionally data-only. Do not force domain behaviour into transport objects.

## Practice exercise

Find business logic that repeatedly reads several fields from one model. Move the rule to that model or to a domain policy that owns the rule.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Data Class](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
