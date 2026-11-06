# Replace Method with Method Object

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Turn a long method with many local variables into an object whose fields hold the intermediate state.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
int price(Order order) {
    int quantity = order.quantity();
    int base = quantity * order.unitPrice();
    int discount = base > 10_000 ? base / 10 : 0;
    int shipping = quantity > 5 ? 0 : 500;
    return base - discount + shipping;
}
```

## After: refactored code

```java
final class OrderPriceCalculator {
    private final Order order;
    private int base;
    private int discount;
    private int shipping;

    OrderPriceCalculator(Order order) { this.order = order; }

    int calculate() {
        calculateBase();
        calculateDiscount();
        calculateShipping();
        return base - discount + shipping;
    }

    private void calculateBase() { base = order.quantity() * order.unitPrice(); }
    private void calculateDiscount() { discount = base > 10_000 ? base / 10 : 0; }
    private void calculateShipping() { shipping = order.quantity() > 5 ? 0 : 500; }
}
```

## Why the refactoring helps

Breaks a difficult algorithm into small methods while giving intermediate values a home.

## When to use it

When a method is too long to decompose cleanly because many local variables are shared between steps.

## Cautions

This adds a class. Use it for genuinely complex calculations, not every long method.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Convert a complex supplier eligibility calculation into a calculator object.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
