# Extract Class

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Create a new class for a coherent group of fields and methods inside an oversized class.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Customer {
    String name;
    String street;
    String city;
    String postalCode;
    String country;
    String formattedAddress() { return street + ", " + city + " " + postalCode; }
}
```

## After: refactored code

```java
class Address {
    private final String street, city, postalCode, country;
    Address(String street, String city, String postalCode, String country) {
        this.street = street; this.city = city; this.postalCode = postalCode; this.country = country;
    }
    String formatted() { return street + ", " + city + " " + postalCode; }
}

class Customer {
    String name;
    Address address;
}
```

## Why the refactoring helps

Creates a clear boundary around a responsibility and reduces the size of the original class.

## When to use it

When a subset of fields and methods forms a meaningful concept with its own rules.

## Cautions

Do not split classes arbitrarily. A new class should represent a stable concept, not just reduce line count.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract bank-account details from Customer into a BankAccount class.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
