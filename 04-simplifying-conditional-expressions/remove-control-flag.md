# Remove Control Flag

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace a boolean flag that controls loop termination or flow with direct control flow.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
boolean found = false;
for (Order order : orders) {
    if (order.id().equals(targetId)) {
        found = true;
        break;
    }
}
return found;
```

## After: refactored code

```java
for (Order order : orders) {
    if (order.id().equals(targetId)) {
        return true;
    }
}
return false;
```

## Why the refactoring helps

Removes a state variable that exists only to communicate a decision already expressible by return, break, or continue.

## When to use it

When a flag is used only to exit a loop or choose a final return.

## Cautions

Preserve cleanup and resource-closing behaviour; direct returns must not bypass required work.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove a found flag from a method that searches a collection.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
