# Push Down Method

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Move a method from a superclass to the subclasses that actually need it.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
abstract class Employee {
    void calculateCommission() { /* used only by Salesperson */ }
}
class Engineer extends Employee {}
class Salesperson extends Employee {}
```

## After: refactored code

```java
abstract class Employee {}
class Engineer extends Employee {}
class Salesperson extends Employee {
    void calculateCommission() { /* sales commission rule */ }
}
```

## Why the refactoring helps

Reduces the superclass API and avoids exposing irrelevant behaviour to all subclasses.

## When to use it

When a method is meaningful only for some subclasses.

## Cautions

If multiple subclasses need variants, consider a strategy or a more accurate intermediate superclass.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Push calculateOvertimePay down to hourly employees if salaried employees never use it.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
