# Collapse Hierarchy

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Remove a superclass or subclass when they no longer represent meaningful differences.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class StandardReport extends Report {
    // No additional state or behaviour.
}
class Report { /* all real behaviour */ }
```

## After: refactored code

```java
class Report { /* all real behaviour */ }
// StandardReport is removed; callers use Report directly.
```

## Why the refactoring helps

Simplifies a hierarchy that has become redundant after requirements changed.

## When to use it

When a subclass or superclass adds no meaningful behaviour, state, or variation.

## Cautions

Update dependency injection bindings, persistence discriminators, and external APIs carefully.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Collapse empty subclasses left behind after a product feature was retired.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
