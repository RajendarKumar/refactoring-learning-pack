# Substitute Algorithm

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace an existing algorithm with a clearer or more efficient one that produces the same result.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
boolean contains(List<String> names, String target) {
    for (String name : names) {
        if (name.equalsIgnoreCase(target)) return true;
    }
    return false;
}
```

## After: refactored code

```java
boolean contains(List<String> names, String target) {
    return names.stream().anyMatch(name -> name.equalsIgnoreCase(target));
}
```

## Why the refactoring helps

A better-known or simpler algorithm can reduce code and make intent obvious.

## When to use it

When a simpler, tested algorithm or library operation exists.

## Cautions

Preserve edge-case behaviour: null handling, ordering, case rules, overflow, and complexity may differ.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace a manual sort or search with a standard library operation and test boundary cases.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
