# Code Smell: Primitive Obsession

**Category:** Bloaters  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Domain concepts are represented by primitive values even though they have their own validation rules, invariants, or behaviour.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The same primitive is passed around with an implicit meaning.
- Validation for an email, currency, identifier, or status is repeated.
- Invalid values can be created and passed deep into the system.

## Before: a problematic design

```java
void registerSupplier(String name, String email, String taxId) {
    if (email == null || !email.contains("@")) {
        throw new IllegalArgumentException("Invalid email");
    }
    // taxId format is checked again in other services...
}
```

## After: a possible refactoring

```java
record EmailAddress(String value) {
    EmailAddress {
        if (value == null || !value.matches("[^@\s]+@[^@\s]+\.[^@\s]+")) {
            throw new IllegalArgumentException("Invalid email");
        }
    }
}

record TaxIdentifier(String value) {
    TaxIdentifier {
        if (value == null || value.isBlank()) {
            throw new IllegalArgumentException("Tax ID is required");
        }
    }
}

void registerSupplier(String name, EmailAddress email, TaxIdentifier taxId) {
    // Inputs are valid domain values at this boundary.
}
```

## Why the refactoring helps

Value objects give a concept a name and place its invariants beside its data. The compiler also prevents accidentally passing an email where a tax identifier is expected.

## Refactorings to consider

- Replace Data Value with Object
- Replace Type Code with Class
- Encapsulate Field

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Not every String or int needs a wrapper. Introduce a value object when the value has domain meaning, validation, formatting, or behaviour. For money, use BigDecimal plus a currency rather than double.

## Practice exercise

Find a primitive used to represent a supplier ID, country code, or money amount. Design a small immutable value object with one or two invariants.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Primitive Obsession](https://refactoring.guru/refactoring/smells/bloaters)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
