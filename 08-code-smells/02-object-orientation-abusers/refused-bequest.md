# Code Smell: Refused Bequest

**Category:** Object-Orientation Abusers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A subclass inherits operations or state that do not make sense for it, often overriding methods to throw exceptions or leaving inherited behaviour unused.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- A subclass throws UnsupportedOperationException for inherited operations.
- The subclass exposes methods it cannot honour.
- The inheritance relationship describes code reuse rather than a true is-a relationship.

## Before: a problematic design

```java
abstract class BankAccount {
    void deposit(BigDecimal amount) { /* add funds */ }
    void withdraw(BigDecimal amount) { /* subtract funds */ }
}

class FixedDepositAccount extends BankAccount {
    @Override
    void withdraw(BigDecimal amount) {
        throw new UnsupportedOperationException("Locked until maturity");
    }
}
```

## After: a possible refactoring

```java
interface Account {
    void deposit(BigDecimal amount);
    BigDecimal balance();
}

interface WithdrawableAccount extends Account {
    void withdraw(BigDecimal amount);
}

class CurrentAccount implements WithdrawableAccount { /* supports deposit and withdrawal */ }
class FixedDepositAccount implements Account { /* deposit and maturity settlement only */ }
```

## Why the refactoring helps

The types now expose only capabilities they can honour. A caller that needs withdrawal can depend on WithdrawableAccount instead of discovering at runtime that one subtype rejects the operation.

## Refactorings to consider

- Replace Inheritance with Delegation
- Extract Interface
- Extract Superclass (only for genuinely shared behaviour)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Unused inherited methods do not always mean the hierarchy is wrong. Check the Liskov Substitution Principle and the domain model before changing inheritance.

## Practice exercise

Find a subclass that disables parent methods. Replace the broad parent contract with smaller capability interfaces or composition.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Refused Bequest](https://refactoring.guru/refactoring/smells/oo-abusers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
