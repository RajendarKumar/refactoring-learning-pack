# Code Smell: Comments

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Comments compensate for unclear code by explaining what a block does instead of letting the code express its intent.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Comments repeat the next line in English.
- A comment is required to understand a complex condition.
- Comments are stale because code changed but the explanation did not.

## Before: a problematic design

```java
// Check whether the order can receive free shipping.
if (order.getTotal().compareTo(new BigDecimal("5000")) >= 0
        && order.getCustomer().isVip()) {
    order.setShippingFee(BigDecimal.ZERO);
}
```

## After: a possible refactoring

```java
if (freeShippingPolicy.isEligible(order)) {
    order.setShippingFee(BigDecimal.ZERO);
}
```

## Why the refactoring helps

A meaningful method name explains the intention and gives the rule a home. Comments remain useful for explaining why a surprising business constraint exists, not for restating what code already says.

## Refactorings to consider

- Extract Method
- Rename Method
- Introduce Assertion (to make an invariant executable)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not delete valuable comments about rationale, legal constraints, workarounds, or non-obvious trade-offs. Improve the code and keep the explanation that cannot be expressed in code.

## Practice exercise

Find three comments that explain what code does. Replace each with a better name, extracted method, or clearer condition. Keep comments that explain why.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Comments](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
