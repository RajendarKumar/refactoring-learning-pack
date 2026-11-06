# Move Method

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move a method to the class that owns most of the data it uses.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    private Customer customer;
    Money customerDiscount() {
        return customer.discountRate().multiply(total());
    }
}
```

## After: refactored code

```java
class Customer {
    Money discountFor(Money orderTotal) {
        return discountRate.multiply(orderTotal);
    }
}

class Order {
    private Customer customer;
    Money customerDiscount() {
        return customer.discountFor(total());
    }
}
```

## Why the refactoring helps

Responsibility moves closer to the data it operates on, reducing feature envy.

## When to use it

When a method uses another object’s data more than its own.

## Cautions

Keep the public API stable with a delegating method when callers need a migration path.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Move supplier risk calculation to the class that owns the supplier risk attributes.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
