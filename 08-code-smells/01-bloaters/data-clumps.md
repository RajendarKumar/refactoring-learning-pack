# Code Smell: Data Clumps

**Category:** Bloaters  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

The same group of values repeatedly travels together through fields, method parameters, or local variables.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- The same three or four parameters appear in multiple methods.
- The same fields are copied between DTOs and service methods.
- Removing one value would make the remaining values less meaningful.

## Before: a problematic design

```java
void createCustomer(String street, String city, String state, String postalCode) { /* ... */ }
void createShipment(String street, String city, String state, String postalCode) { /* ... */ }
String formatAddress(String street, String city, String state, String postalCode) { /* ... */ }
```

## After: a possible refactoring

```java
record Address(String street, String city, String state, String postalCode) {
    String format() {
        return street + ", " + city + ", " + state + " " + postalCode;
    }
}

void createCustomer(Address address) { /* ... */ }
void createShipment(Address destination) { /* ... */ }
String formatAddress(Address address) { return address.format(); }
```

## Why the refactoring helps

The values now form one cohesive concept. This reduces parameter noise and centralizes address-specific behaviour.

## Refactorings to consider

- Introduce Parameter Object
- Extract Class
- Preserve Whole Object

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not group values merely because they have the same primitive type. Group them because they form a real concept and change together.

## Practice exercise

Search for repeated parameter groups in your codebase. Choose one group and replace it with a domain record.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Data Clumps](https://refactoring.guru/refactoring/smells/bloaters)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
