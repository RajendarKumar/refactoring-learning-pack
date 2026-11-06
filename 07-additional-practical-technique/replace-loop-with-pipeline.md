# Replace Loop with Pipeline

> Category: Additional Practical Technique  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: Additional practical technique; not part of the 66 Refactoring.Guru entries.

## Intent

Replace a manual collection-processing loop with a sequence of filter, map, and terminal operations.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
List<String> names = new ArrayList<>();
for (Order order : orders) {
    if (order.status() == OrderStatus.PAID) {
        names.add(order.customerName().toUpperCase());
    }
}
```

## After: refactored code

```java
List<String> names = orders.stream()
        .filter(order -> order.status() == OrderStatus.PAID)
        .map(order -> order.customerName().toUpperCase())
        .toList();
```

## Why the refactoring helps

The pipeline expresses the data transformation declaratively and separates selection from mapping.

## When to use it

When a loop transforms or filters a collection without complex mutable state.

## Cautions

Keep loops for complex control flow, checked exceptions, early exits, or performance-sensitive cases where a stream obscures intent. Consider null handling and encounter order.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Rewrite a loop that selects active suppliers and maps them to supplier IDs using Stream operations.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
