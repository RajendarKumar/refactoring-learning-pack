# Code Smell: Inappropriate Intimacy

**Category:** Couplers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

Two classes know too much about each other’s internal representation and depend on private or low-level details.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- One class modifies another class’s internal collection directly.
- Classes are tightly coupled to each other’s fields and construction details.
- A change to an internal representation forces changes in a neighbour.

## Before: a problematic design

```java
class OrderService {
    void addOrder(Customer customer, Order order) {
        customer.orders.add(order);       // package-private internal collection
        order.customer = customer;        // direct mutation of another object's field
        customer.orderCount++;
    }
}
```

## After: a possible refactoring

```java
class Customer {
    private final List<Order> orders = new ArrayList<>();

    void addOrder(Order order) {
        orders.add(order);
        order.assignCustomer(this);
    }
}

class Order {
    private Customer customer;
    void assignCustomer(Customer customer) { this.customer = customer; }
}

class OrderService {
    void addOrder(Customer customer, Order order) {
        customer.addOrder(order);
    }
}
```

## Why the refactoring helps

Each object owns the operation that protects its invariants. Callers no longer coordinate internal field updates themselves.

## Refactorings to consider

- Encapsulate Collection
- Move Method
- Move Field
- Hide Delegate
- Change Bidirectional Association to Unidirectional

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Bidirectional relationships may be required by an ORM or domain model. Encapsulate their updates and define one clear owner; do not remove a necessary relationship blindly.

## Practice exercise

Find a class that manipulates another object’s fields or collection. Replace direct mutation with a behaviour method and test the invariant.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Inappropriate Intimacy](https://refactoring.guru/refactoring/smells/couplers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
