# Code Smell: Parallel Inheritance Hierarchies

**Category:** Change Preventers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Creating a subclass in one hierarchy repeatedly requires a matching subclass in another hierarchy.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Every Payment subtype has a corresponding ReceiptSender subtype.
- Two inheritance trees grow in lockstep.
- A new domain variation requires edits in multiple class hierarchies.

## Before: a problematic design

```java
abstract class Payment { }
class CardPayment extends Payment { }
class WalletPayment extends Payment { }

abstract class ReceiptSender { }
class CardReceiptSender extends ReceiptSender { }
class WalletReceiptSender extends ReceiptSender { }
```

## After: a possible refactoring

```java
interface ReceiptSender {
    void sendReceipt(Payment payment);
}

class Payment {
    private final ReceiptSender receiptSender;

    Payment(ReceiptSender receiptSender) {
        this.receiptSender = receiptSender;
    }

    void complete() {
        // complete payment
        receiptSender.sendReceipt(this);
    }
}
```

## Why the refactoring helps

The second hierarchy becomes a replaceable collaborator. Payment variations no longer force one-to-one subclass creation in a separate tree.

## Refactorings to consider

- Replace Inheritance with Delegation
- Move Method
- Move Field

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

A pair of hierarchies is not automatically wrong. The smell appears when they must evolve in lockstep and the relationship adds coordination cost.

## Practice exercise

Find two parallel type hierarchies. Choose one axis of variation and replace its inheritance tree with a composed strategy or collaborator.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Parallel Inheritance Hierarchies](https://refactoring.guru/refactoring/smells/change-preventers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
