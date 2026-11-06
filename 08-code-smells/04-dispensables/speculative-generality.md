# Code Smell: Speculative Generality

**Category:** Dispensables  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Abstractions, extension points, parameters, or hooks exist for hypothetical future needs rather than current requirements.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- An abstract class has only one implementation and no concrete variation is expected.
- Methods or parameters are never used.
- Several layers of indirection exist “in case” another use case appears.

## Before: a problematic design

```java
abstract class BaseSupplierExporter<T> {
    protected void beforeExport(T value) { }
    protected void afterExport(T value) { }
    abstract byte[] export(T value);
}

class CsvSupplierExporter extends BaseSupplierExporter<Supplier> {
    @Override byte[] export(Supplier supplier) { return toCsv(supplier); }
}
```

## After: a possible refactoring

```java
class CsvSupplierExporter {
    byte[] export(Supplier supplier) {
        return toCsv(supplier);
    }
}
```

## Why the refactoring helps

The design reflects the requirement that exists today. If a second exporter or real extension point appears, the abstraction can be introduced with evidence and concrete use cases.

## Refactorings to consider

- Inline Class
- Inline Method
- Collapse Hierarchy
- Remove Parameter

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not remove a proven architectural extension point merely because it currently has one implementation. Consider plugin systems, dependency inversion boundaries, tests, and planned integrations backed by committed requirements.

## Practice exercise

Find an unused hook, generic parameter, or abstract layer. Identify a real current caller for it. If none exists, simplify the design and keep the change reversible.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Speculative Generality](https://refactoring.guru/refactoring/smells/dispensables)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
