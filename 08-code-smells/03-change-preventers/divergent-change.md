# Code Smell: Divergent Change

**Category:** Change Preventers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

One class is frequently modified for several unrelated reasons, so changes to one responsibility risk disturbing another.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- A class changes for CSV format, compliance rules, persistence, and email wording.
- Different stakeholders request unrelated edits to the same class.
- The class has multiple independent reasons to change.

## Before: a problematic design

```java
class SupplierService {
    Supplier importCsv(byte[] file) { /* CSV parsing */ }
    void validate(Supplier supplier) { /* country compliance rules */ }
    void save(Supplier supplier) { /* database persistence */ }
    void notifySupplier(Supplier supplier) { /* email template */ }
}
```

## After: a possible refactoring

```java
class SupplierImportService {
    private final SupplierCsvParser parser;
    private final SupplierComplianceValidator validator;
    private final SupplierRepository repository;
    private final SupplierNotifier notifier;

    Supplier importAndActivate(byte[] file) {
        Supplier supplier = parser.parse(file);
        validator.validate(supplier);
        repository.save(supplier);
        notifier.sendWelcome(supplier);
        return supplier;
    }
}
```

## Why the refactoring helps

Each collaborator has one main reason to change. The use-case service coordinates the workflow while file formats, business rules, storage, and communication evolve separately.

## Refactorings to consider

- Extract Class
- Move Method
- Move Field

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not split a class solely because it has many methods. Separate responsibilities when they change for different reasons or can be understood independently.

## Practice exercise

Review the last five changes to a large service. Group them by reason for change and propose a class boundary for each unrelated group.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Divergent Change](https://refactoring.guru/refactoring/smells/change-preventers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
