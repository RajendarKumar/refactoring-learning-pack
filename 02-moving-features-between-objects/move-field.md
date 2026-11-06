# Move Field

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move a field to the class that uses or owns it most naturally.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    private String customerTaxRegion;
    Money tax() { return taxService.taxFor(customerTaxRegion, total()); }
}
```

## After: refactored code

```java
class Customer {
    private String taxRegion;
    String taxRegion() { return taxRegion; }
}

class Order {
    private Customer customer;
    Money tax() { return taxService.taxFor(customer.taxRegion(), total()); }
}
```

## Why the refactoring helps

Places data with the domain object responsible for its meaning and lifecycle.

## When to use it

When a field is mostly used by another class or conceptually belongs there.

## Cautions

Consider persistence schemas, serialization, API contracts, and migration of existing data.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Move preferredLanguage from an invoice to the customer if it is a customer attribute.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
