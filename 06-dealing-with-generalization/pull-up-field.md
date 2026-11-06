# Pull Up Field

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move identical fields from sibling subclasses into their common superclass.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Engineer extends Employee { String employeeId; }
class Analyst extends Employee { String employeeId; }
```

## After: refactored code

```java
class Employee { protected String employeeId; }
class Engineer extends Employee {}
class Analyst extends Employee {}
```

## Why the refactoring helps

Removes duplication and establishes a shared representation for a true common attribute.

## When to use it

When sibling subclasses define the same field with the same meaning and lifecycle.

## Cautions

Check whether the field really has identical semantics, visibility, and nullability in all subclasses.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Move common createdAt fields from several event subclasses into Event.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
