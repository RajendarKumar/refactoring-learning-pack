# Pull Up Method

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Move duplicate methods from sibling subclasses into their superclass.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class CardPayment extends Payment {
    Money fee() { return amount.multiply(new BigDecimal("0.02")); }
}
class WalletPayment extends Payment {
    Money fee() { return amount.multiply(new BigDecimal("0.02")); }
}
```

## After: refactored code

```java
abstract class Payment {
    protected Money amount;
    Money fee() { return amount.multiply(new BigDecimal("0.02")); }
}
class CardPayment extends Payment {}
class WalletPayment extends Payment {}
```

## Why the refactoring helps

Places identical behaviour in one shared implementation.

## When to use it

When methods are identical or can be made identical with a small generalization.

## Cautions

Do not pull up methods whose apparent similarity hides different business rules.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Move duplicate validation logic from two supplier channel subclasses into a base class.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
