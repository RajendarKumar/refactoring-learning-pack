# Replace Array with Object

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace a positional array with a class or record whose fields have names.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Object[] row = {"PO-12", "OPEN", 3};
String id = (String) row[0];
String status = (String) row[1];
```

## After: refactored code

```java
record PurchaseOrderRow(String id, String status, int lineCount) {}

PurchaseOrderRow row = new PurchaseOrderRow("PO-12", "OPEN", 3);
String id = row.id();
String status = row.status();
```

## Why the refactoring helps

Named fields remove index-based knowledge and unsafe casts.

## When to use it

When an array always stores the same kinds of values at fixed positions.

## Cautions

For collections of homogeneous values, keep using arrays or lists. This technique targets tuple-like structures.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace an Object[] report row with a typed record.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
