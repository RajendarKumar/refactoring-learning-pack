# Replace Conditional with Polymorphism

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move type-dependent branches into implementations of a common interface.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
int fee(Shipment shipment) {
    return switch (shipment.type()) {
        case AIR -> shipment.weight() * 10;
        case ROAD -> shipment.weight() * 4;
    };
}
```

## After: refactored code

```java
interface ShippingPolicy { int fee(Shipment shipment); }
final class AirShippingPolicy implements ShippingPolicy {
    public int fee(Shipment s) { return s.weight() * 10; }
}
final class RoadShippingPolicy implements ShippingPolicy {
    public int fee(Shipment s) { return s.weight() * 4; }
}
```

## Why the refactoring helps

Each variation owns its calculation, and new variants can be added with less modification to existing code.

## When to use it

When a switch repeatedly selects behaviour based on a stable type hierarchy or strategy.

## Cautions

Not every switch needs polymorphism. Enums and simple switches are often clearer for small, stable cases.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Refactor payment-channel-specific fee logic into PaymentFeePolicy implementations.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
