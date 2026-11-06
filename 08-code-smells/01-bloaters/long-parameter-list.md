# Code Smell: Long Parameter List

**Category:** Bloaters  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A method requires many independent arguments, making calls difficult to read and easy to get wrong.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Call sites contain several adjacent Strings, dates, or numbers.
- Callers repeatedly pass the same group of arguments.
- Adding one new field forces changes to many method signatures.

## Before: a problematic design

```java
Shipment createShipment(
        String supplierId,
        String originCountry,
        String originPostalCode,
        String destinationCountry,
        String destinationPostalCode,
        LocalDate shipDate,
        BigDecimal weight) {
    // create shipment
}
```

## After: a possible refactoring

```java
record Address(String country, String postalCode) {}

record ShipmentRequest(
        String supplierId,
        Address origin,
        Address destination,
        LocalDate shipDate,
        BigDecimal weight) {}

Shipment createShipment(ShipmentRequest request) {
    // request.origin(), request.destination(), etc.
}
```

## Why the refactoring helps

The request object groups related data, names the operation’s input, and gives future fields one natural place to live.

## Refactorings to consider

- Introduce Parameter Object
- Preserve Whole Object

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not create a generic bag of unrelated fields. The parameter object should represent a meaningful request or domain concept. Avoid mutable request objects unless mutation is intentional.

## Practice exercise

Convert a method with six or more parameters into a request record. Update call sites and add tests for invalid combinations.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Long Parameter List](https://refactoring.guru/refactoring/smells/bloaters)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
