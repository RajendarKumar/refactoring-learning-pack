# Replace Type Code with State/Strategy

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace a type flag that changes behaviour with a state or strategy object.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    String status;
    void ship() {
        if (status.equals("PAID")) status = "SHIPPED";
        else throw new IllegalStateException();
    }
}
```

## After: refactored code

```java
interface OrderState {
    OrderState ship();
}
final class PaidState implements OrderState {
    public OrderState ship() { return new ShippedState(); }
}
final class ShippedState implements OrderState {
    public OrderState ship() { throw new IllegalStateException("already shipped"); }
}
```

## Why the refactoring helps

Encapsulates state-dependent behaviour and valid transitions instead of scattering conditionals.

## When to use it

When behaviour and allowed operations depend heavily on the current state or selected strategy.

## Cautions

Use a full State pattern only when state-specific behaviour justifies the extra types.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Model a supplier onboarding workflow with Draft, Submitted, and Approved states.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
