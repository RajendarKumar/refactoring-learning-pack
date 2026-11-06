# Introduce Null Object

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace repeated null checks with an object that provides safe default behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
String phone = customer == null ? "N/A" : customer.phone();
```

## After: refactored code

```java
interface CustomerInfo { String phone(); }
final class RealCustomer implements CustomerInfo {
    public String phone() { return phoneNumber; }
}
final class MissingCustomer implements CustomerInfo {
    public String phone() { return "N/A"; }
}

String phone = customerInfo.phone();
```

## Why the refactoring helps

Encapsulates absence behaviour and reduces repeated null branching.

## When to use it

When absence is expected and has a stable, meaningful default behaviour.

## Cautions

Do not hide unexpected missing data or use a fake object where absence must trigger an error.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Introduce an UnknownSupplier object for optional supplier display information.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
