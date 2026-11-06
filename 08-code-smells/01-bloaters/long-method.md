# Code Smell: Long Method

**Category:** Bloaters  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A method accumulates too many steps or responsibilities, so its intent is difficult to see and individual parts are hard to test.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- You must scroll repeatedly to understand one operation.
- The method mixes validation, calculation, persistence, and notification.
- Comments are needed to explain separate sections of the method.

## Before: a problematic design

```java
class OrderService {
    void placeOrder(Order order) {
        if (order.items().isEmpty()) {
            throw new IllegalArgumentException("Order is empty");
        }

        BigDecimal subtotal = order.items().stream()
                .map(item -> item.price().multiply(BigDecimal.valueOf(item.quantity())))
                .reduce(BigDecimal.ZERO, BigDecimal::add);

        BigDecimal discount = subtotal.compareTo(new BigDecimal("1000")) >= 0
                ? subtotal.multiply(new BigDecimal("0.10"))
                : BigDecimal.ZERO;
        BigDecimal total = subtotal.subtract(discount);

        paymentGateway.charge(order.customerId(), total);
        order.markPaid(total);
        orderRepository.save(order);
        emailClient.sendConfirmation(order.customerEmail(), total);
    }
}
```

## After: a possible refactoring

```java
class OrderService {
    void placeOrder(Order order) {
        validateOrder(order);
        BigDecimal total = calculateTotal(order);
        collectPayment(order, total);
        persistOrder(order);
        sendConfirmation(order, total);
    }

    private void validateOrder(Order order) {
        if (order.items().isEmpty()) {
            throw new IllegalArgumentException("Order is empty");
        }
    }

    private BigDecimal calculateTotal(Order order) {
        BigDecimal subtotal = order.items().stream()
                .map(item -> item.price().multiply(BigDecimal.valueOf(item.quantity())))
                .reduce(BigDecimal.ZERO, BigDecimal::add);
        BigDecimal discount = subtotal.compareTo(new BigDecimal("1000")) >= 0
                ? subtotal.multiply(new BigDecimal("0.10")) : BigDecimal.ZERO;
        return subtotal.subtract(discount);
    }

    // collectPayment, persistOrder, and sendConfirmation each own one step.
}
```

## Why the refactoring helps

The top-level method now reads like a business workflow. Each extracted method has one clear purpose and can be tested independently. If a section grows or owns a different responsibility, it may become a collaborator rather than another private helper.

## Refactorings to consider

- Extract Method
- Decompose Conditional
- Replace Method with Method Object (when extracted logic needs substantial local state)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Do not split code into tiny methods that merely hide simple expressions. Extract around meaningful domain steps, not arbitrary line counts.

## Practice exercise

Extract validation, total calculation, and confirmation from a long invoice-generation method. Add tests proving that validation still happens before payment.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Long Method](https://refactoring.guru/refactoring/smells/bloaters)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
