# Inline Class

> Category: Moving Features Between Objects  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move the responsibilities of a class into its caller and remove the class when it no longer adds value.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class ContactInfo {
    private String phone;
    String phone() { return phone; }
}

class Customer {
    private ContactInfo contactInfo;
    String phone() { return contactInfo.phone(); }
}
```

## After: refactored code

```java
class Customer {
    private String phone;
    String phone() { return phone; }
}
```

## Why the refactoring helps

Reduces needless indirection when a class has become too small or has no independent responsibility.

## When to use it

When a class is merely a pass-through wrapper and its responsibilities clearly belong elsewhere.

## Cautions

Do not inline a class that provides an important domain boundary, lifecycle, or independent variation point.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Identify a one-field wrapper in a small domain model and decide whether it deserves to exist.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
