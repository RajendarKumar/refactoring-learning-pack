# Introduce Parameter Object

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Group parameters that naturally travel together into one domain object.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
List<Order> search(LocalDate from, LocalDate to, String country, OrderStatus status) { ... }
```

## After: refactored code

```java
record OrderSearchCriteria(LocalDate from, LocalDate to, String country, OrderStatus status) {}

List<Order> search(OrderSearchCriteria criteria) { ... }
```

## Why the refactoring helps

Reduces long parameter lists and gives a reusable name to a cohesive set of query criteria.

## When to use it

When multiple parameters form a concept and appear together in several methods.

## Cautions

Do not group unrelated parameters just to reduce method signatures; validate the new object at its boundary.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Create SupplierSearchCriteria from repeated supplier query parameters.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
