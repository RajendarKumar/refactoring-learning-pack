# Hide Delegate

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Make a class provide the operation clients need instead of exposing an internal object chain.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
String city = order.customer().address().city();
```

## After: refactored code

```java
class Order {
    private Customer customer;
    String customerCity() { return customer.address().city(); }
}

String city = order.customerCity();
```

## Why the refactoring helps

Prevents clients from depending on the internal structure of an object graph.

## When to use it

When many clients navigate through the same delegate chain.

## Cautions

Avoid creating a large forwarding API. Expose domain operations rather than every field of the delegate.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Hide the path from PurchaseOrder to Supplier to Address from UI callers.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
