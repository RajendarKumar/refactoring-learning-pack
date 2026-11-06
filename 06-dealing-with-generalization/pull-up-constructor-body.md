# Pull Up Constructor Body

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Move common constructor initialization into a superclass constructor or shared initialization method.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class CardPayment extends Payment {
    CardPayment(String id, Money amount) { this.id = id; this.amount = amount; this.createdAt = Instant.now(); }
}
class BankPayment extends Payment {
    BankPayment(String id, Money amount) { this.id = id; this.amount = amount; this.createdAt = Instant.now(); }
}
```

## After: refactored code

```java
abstract class Payment {
    protected final String id;
    protected final Money amount;
    protected final Instant createdAt;
    Payment(String id, Money amount) {
        this.id = id; this.amount = amount; this.createdAt = Instant.now();
    }
}
class CardPayment extends Payment {
    CardPayment(String id, Money amount) { super(id, amount); }
}
```

## Why the refactoring helps

Centralizes common initialization and ensures all subclasses establish the same base invariants.

## When to use it

When subclass constructors repeat the same initialization steps.

## Cautions

Be careful with overridable method calls from constructors and initialization order.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Move repeated id and timestamp initialization into a shared base event constructor.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
