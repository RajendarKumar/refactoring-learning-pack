# Code Smell: Message Chains

**Category:** Couplers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A caller navigates through a chain of objects to reach data or behaviour several relationships away.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Calls look like a.getB().getC().getD().value().
- Client code knows the internal object graph.
- A relationship change requires edits in many clients.

## Before: a problematic design

```java
String taxRegion = order.getCustomer()
        .getAddress()
        .getCountry()
        .getTaxRegion();
```

## After: a possible refactoring

```java
String taxRegion = order.taxRegion();

class Order {
    private Customer customer;

    String taxRegion() {
        return customer.taxRegion();
    }
}

class Customer {
    private Address address;
    String taxRegion() {
        return address.country().taxRegion();
    }
}
```

## Why the refactoring helps

The client asks the object it knows for the domain information it needs. Internal navigation is hidden behind a meaningful operation.

## Refactorings to consider

- Hide Delegate
- Move Method

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not create a long sequence of pass-through methods that merely hide every dot. Expose meaningful domain behaviour or a stable value, not a mechanical copy of the object graph.

## Practice exercise

Find a message chain in a service. Replace it with one domain-oriented method at the object boundary that should own the knowledge.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Message Chains](https://refactoring.guru/refactoring/smells/couplers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
