# Replace Inheritance with Delegation

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Replace subclassing with a contained object when the subclass uses only part of the parent or inherits unwanted behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Stack extends ArrayList<String> {
    void push(String value) { add(value); }
    String pop() { return remove(size() - 1); }
}
```

## After: refactored code

```java
class Stack {
    private final List<String> items = new ArrayList<>();
    void push(String value) { items.add(value); }
    String pop() { return items.remove(items.size() - 1); }
}
```

## Why the refactoring helps

Exposes only the intended stack operations instead of the entire List API.

## When to use it

When inheritance violates substitutability or exposes operations the subtype should not support.

## Cautions

Delegation requires forwarding methods but gives stronger control over the public contract.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace a specialised cache subclass of HashMap with a Cache that delegates to a private Map.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
