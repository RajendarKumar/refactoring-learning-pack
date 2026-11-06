# Remove Middle Man

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Let clients call the delegate directly when a class only forwards many operations.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    private Customer customer;
    String name() { return customer.name(); }
    String email() { return customer.email(); }
    String phone() { return customer.phone(); }
}

String email = order.email();
```

## After: refactored code

```java
class Order {
    Customer customer() { return customer; }
}

String email = order.customer().email();
```

## Why the refactoring helps

Reduces a forwarding layer that adds no meaningful protection or behaviour.

## When to use it

When a class contains many methods that merely delegate to another object.

## Cautions

This trades encapsulation for fewer forwarding methods. Use only when the delegate is a stable part of the model.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Count forwarding methods in a facade-like entity and remove only those that add no policy.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
