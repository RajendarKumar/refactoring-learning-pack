# Code Smell: Feature Envy

**Category:** Couplers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A method seems more interested in another object’s data than in the data of the class where the method lives.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- A method calls many getters on one collaborator.
- The method contains calculations based mostly on another object’s fields.
- Changing the collaborator’s data structure repeatedly breaks this method.

## Before: a problematic design

```java
class InvoiceService {
    BigDecimal discountFor(Customer customer, BigDecimal subtotal) {
        if (customer.getTier() == CustomerTier.GOLD && customer.getLoyaltyPoints() > 1000) {
            return subtotal.multiply(new BigDecimal("0.15"));
        }
        return BigDecimal.ZERO;
    }
}
```

## After: a possible refactoring

```java
class Customer {
    BigDecimal discountFor(BigDecimal subtotal) {
        if (tier == CustomerTier.GOLD && loyaltyPoints > 1000) {
            return subtotal.multiply(new BigDecimal("0.15"));
        }
        return BigDecimal.ZERO;
    }
}

class InvoiceService {
    BigDecimal discountFor(Customer customer, BigDecimal subtotal) {
        return customer.discountFor(subtotal);
    }
}
```

## Why the refactoring helps

The calculation moves next to the information it uses. Customer’s policy is encapsulated instead of being reconstructed by unrelated callers.

## Refactorings to consider

- Move Method
- Move Field
- Extract Class (when the behaviour belongs to a separate domain policy)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not move a method just because it reads another object. If it coordinates several domain objects or represents an application use case, the service may be the correct home.

## Practice exercise

Inspect one method with many calls to a single collaborator. Decide whether it is a domain behaviour of that collaborator or an orchestration responsibility.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Feature Envy](https://refactoring.guru/refactoring/smells/couplers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
