# Introduce Local Extension

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Create a wrapper or subclass in your own code to add several related operations to a library class.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
// Many services repeatedly combine library calls for a domain-specific date rule.
LocalDate dueDate = invoiceDate.plusDays(30);
boolean overdue = dueDate.isBefore(today);
```

## After: refactored code

```java
final class BusinessDate {
    private final LocalDate value;
    BusinessDate(LocalDate value) { this.value = value; }
    BusinessDate plusPaymentTerms(int days) { return new BusinessDate(value.plusDays(days)); }
    boolean isBefore(LocalDate date) { return value.isBefore(date); }
    LocalDate value() { return value; }
}

BusinessDate dueDate = new BusinessDate(invoiceDate).plusPaymentTerms(30);
```

## Why the refactoring helps

Groups several related extensions behind a type owned by the application.

## When to use it

When multiple helper operations belong together and are used repeatedly.

## Cautions

Prefer composition over subclassing library types; preserve equality and conversion semantics deliberately.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Create a Money or BusinessDate wrapper for repeated domain-specific behaviour.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
