# Code Smell: Shotgun Surgery

**Category:** Change Preventers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

One business change forces many small edits across different classes and modules.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The same formula or rule is copied into multiple services.
- A small policy change requires editing many files.
- Developers regularly miss one of the duplicated locations.

## Before: a problematic design

```java
class OrderService {
    BigDecimal tax(BigDecimal amount) { return amount.multiply(new BigDecimal("0.18")); }
}
class InvoiceService {
    BigDecimal tax(BigDecimal amount) { return amount.multiply(new BigDecimal("0.18")); }
}
class RefundService {
    BigDecimal tax(BigDecimal amount) { return amount.multiply(new BigDecimal("0.18")); }
}
```

## After: a possible refactoring

```java
class TaxPolicy {
    BigDecimal calculate(BigDecimal taxableAmount) {
        return taxableAmount.multiply(new BigDecimal("0.18"));
    }
}

class OrderService {
    private final TaxPolicy taxPolicy;
    BigDecimal tax(BigDecimal amount) { return taxPolicy.calculate(amount); }
}
// InvoiceService and RefundService use the same TaxPolicy. Only one policy owns the rate.
```

## Why the refactoring helps

The rule has one source of truth. A tax-rate change is made in one policy rather than coordinated edits to many services.

## Refactorings to consider

- Move Method
- Extract Class
- Pull Up Method (when duplicate behaviour belongs in a shared superclass)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Avoid centralizing formulas that only look similar but have different legal or business meanings. Confirm the rule is genuinely shared before unifying it.

## Practice exercise

Search for a business constant or formula duplicated in several files. Identify whether all occurrences represent the same policy and centralize only that policy.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Shotgun Surgery](https://refactoring.guru/refactoring/smells/change-preventers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
