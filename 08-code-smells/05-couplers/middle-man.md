# Code Smell: Middle Man

**Category:** Couplers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A class delegates most or all work to another class without adding policy, coordination, or a useful abstraction.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Nearly every method consists of one forwarding call.
- The class has no independent state or rules.
- Callers must navigate an extra layer that adds no meaningful boundary.

## Before: a problematic design

```java
class SupplierService {
    private final SupplierRepository repository;

    Supplier findById(String id) { return repository.findById(id); }
    void save(Supplier supplier) { repository.save(supplier); }
    void delete(String id) { repository.delete(id); }
}
```

## After: a possible refactoring

```java
class SupplierController {
    private final SupplierRepository repository;

    Supplier getSupplier(String id) {
        return repository.findById(id);
    }
}
```

## Why the refactoring helps

The pass-through service is removed when it has no useful responsibility. The client depends directly on the collaborator it already needs.

## Refactorings to consider

- Remove Middle Man
- Inline Class

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

A service is not a middle man when it enforces authorization, transactions, validation, orchestration, or a stable boundary around infrastructure. Do not bypass meaningful application layers.

## Practice exercise

Review a service whose methods mostly delegate. List any policies it applies. If the list is empty, consider removing the wrapper and updating its callers.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Middle Man](https://refactoring.guru/refactoring/smells/couplers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
