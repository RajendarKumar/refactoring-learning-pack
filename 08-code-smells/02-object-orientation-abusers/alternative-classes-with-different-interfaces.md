# Code Smell: Alternative Classes with Different Interfaces

**Category:** Object-Orientation Abusers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Two classes perform the same role but expose different method names or signatures, making clients handle equivalent objects differently.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Similar implementations use calculate(), compute(), and execute() for the same operation.
- Callers need adapters or branching merely to invoke equivalent services.
- Swapping implementations requires changing client code.

## Before: a problematic design

```java
class DomesticTaxService {
    BigDecimal calculateTax(BigDecimal amount) { return amount.multiply(new BigDecimal("0.10")); }
}

class CrossBorderTaxService {
    BigDecimal computeTax(BigDecimal amount) { return amount.multiply(new BigDecimal("0.15")); }
}
```

## After: a possible refactoring

```java
interface TaxCalculator {
    BigDecimal calculateTax(BigDecimal amount);
}

class DomesticTaxService implements TaxCalculator {
    public BigDecimal calculateTax(BigDecimal amount) {
        return amount.multiply(new BigDecimal("0.10"));
    }
}

class CrossBorderTaxService implements TaxCalculator {
    public BigDecimal calculateTax(BigDecimal amount) {
        return amount.multiply(new BigDecimal("0.15"));
    }
}
```

## Why the refactoring helps

A common contract lets clients use either implementation without knowing its concrete class. Renaming equivalent operations is often the first step; an interface makes the shared role explicit.

## Refactorings to consider

- Rename Method
- Extract Interface
- Unify Interfaces with Adapter (when external APIs cannot be changed)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not force unrelated classes into one interface just because one method name matches. The semantics and contract must genuinely be the same.

## Practice exercise

Identify two implementations that serve the same client role but use different method names. Define a shared interface and adapt legacy callers.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Alternative Classes with Different Interfaces](https://refactoring.guru/refactoring/smells/oo-abusers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
