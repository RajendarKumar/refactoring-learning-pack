# Duplicate Observed Data

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Copy domain data into a presentation or reporting model when that layer cannot directly observe the domain object.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    private Customer customer;
    String customerName() { return customer.name(); }
}
// A remote UI needs customerName in its own read model.
```

## After: refactored code

```java
record OrderView(String orderId, String customerName, BigDecimal total) {}

OrderView toView(Order order) {
    return new OrderView(order.id(), order.customer().name(), order.total());
}
```

## Why the refactoring helps

Creates a local representation for a layer that needs to display or query the data independently.

## When to use it

When UI, reporting, or integration layers need a projection of domain state.

## Cautions

Define how and when copied data is refreshed; duplicated observations can become stale.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Create a response DTO containing supplier display name and onboarding status.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
