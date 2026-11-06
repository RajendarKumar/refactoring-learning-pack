# Replace Subclass with Fields

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Remove trivial subclasses whose only difference is constant data, and represent that data as fields.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class GoldCustomer extends Customer {}
class SilverCustomer extends Customer {}
// Each subclass only overrides discountRate().
```

## After: refactored code

```java
class Customer {
    private final CustomerTier tier;
    Customer(CustomerTier tier) { this.tier = tier; }
    BigDecimal discountRate() { return tier.discountRate(); }
}
enum CustomerTier { GOLD, SILVER }
```

## Why the refactoring helps

Reduces a class hierarchy that encodes only data rather than varying behaviour.

## When to use it

When subclasses differ only by constants or simple properties.

## Cautions

Keep subclasses when they have distinct behaviour, invariants, or lifecycle.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Collapse employee subclasses that only supply a fixed hourly rate into a typed rate field.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
