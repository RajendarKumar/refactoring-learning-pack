# Replace Type Code with Class

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace a primitive code with a small type that represents the category.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Payment {
    static final int CARD = 1;
    static final int BANK = 2;
    int paymentType;
}
```

## After: refactored code

```java
enum PaymentType { CARD, BANK }

class Payment {
    private PaymentType paymentType;
}
```

## Why the refactoring helps

Prevents invalid numeric values and makes call sites self-documenting.

## When to use it

When a primitive represents a fixed set of named values.

## Cautions

Use an enum for a closed set; use a richer class when values are extensible or carry data.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace integer supplier statuses with a SupplierStatus enum.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
