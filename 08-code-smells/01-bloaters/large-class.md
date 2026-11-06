# Code Smell: Large Class

**Category:** Bloaters  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

One class owns too many fields and behaviours, often changing for unrelated reasons.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The class has many unrelated dependencies.
- Different teams or features edit the same class for unrelated reasons.
- The class name ends in Manager, Handler, or Service but covers many domains.

## Before: a problematic design

```java
class SupplierManager {
    void importCsv(byte[] file) { /* parse CSV and map supplier fields */ }
    void validateTaxRegistration(Supplier supplier) { /* country tax rules */ }
    void verifyBankAccount(Supplier supplier) { /* bank verification API */ }
    void storeDocuments(Supplier supplier) { /* document storage */ }
    void sendWelcomeEmail(Supplier supplier) { /* email template and delivery */ }
    void updateSearchIndex(Supplier supplier) { /* search indexing */ }
}
```

## After: a possible refactoring

```java
class SupplierOnboardingService {
    private final SupplierImporter importer;
    private final SupplierComplianceService compliance;
    private final SupplierBankVerification bankVerification;
    private final SupplierDocumentService documents;
    private final SupplierNotifier notifier;

    void onboard(byte[] file) {
        Supplier supplier = importer.importSupplier(file);
        compliance.validate(supplier);
        bankVerification.verify(supplier);
        documents.store(supplier);
        notifier.sendWelcome(supplier);
    }
}
```

## Why the refactoring helps

Responsibilities move to cohesive collaborators. The orchestration service remains, but its job is coordinating the use case rather than implementing every detail.

## Refactorings to consider

- Extract Class
- Move Method
- Move Field

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not create one class per method. A new class should own a coherent concept, state, or reason to change. Keep orchestration where it clarifies the use case.

## Practice exercise

Choose a class in your project with three unrelated responsibilities. Propose the new classes and identify which dependency belongs to each.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Large Class](https://refactoring.guru/refactoring/smells/bloaters)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
