# Replace Parameter with Method Call

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Remove a parameter that the receiving object can calculate from data it already owns.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    Money discountedTotal(Customer customer) {
        return total.multiply(customer.discountRate());
    }
}
```

## After: refactored code

```java
class Order {
    private Customer customer;
    Money discountedTotal() {
        return total.multiply(customer.discountRate());
    }
}
```

## Why the refactoring helps

Reduces argument duplication and keeps derived data next to the state needed to calculate it.

## When to use it

When callers repeatedly pass a value the receiver can reliably derive.

## Cautions

Keep the parameter if callers need to supply a snapshot, alternate policy, or value from another consistency boundary.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove a repeated supplierRegion parameter when the Order already owns its Supplier.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
