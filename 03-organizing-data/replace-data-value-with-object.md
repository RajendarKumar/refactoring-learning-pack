# Replace Data Value with Object

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace a primitive field with a small class that can own validation and behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Order {
    private String phoneNumber;
}
```

## After: refactored code

```java
record PhoneNumber(String value) {
    PhoneNumber {
        if (value == null || value.isBlank()) throw new IllegalArgumentException("phone required");
    }
}

class Order {
    private PhoneNumber phoneNumber;
}
```

## Why the refactoring helps

Encodes domain meaning and validation in the type system.

## When to use it

When a primitive has domain rules, formatting, validation, or operations.

## Cautions

Keep the value object focused. Avoid building a class around every primitive without domain benefit.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace supplierTaxId String with a validated SupplierTaxId type.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
