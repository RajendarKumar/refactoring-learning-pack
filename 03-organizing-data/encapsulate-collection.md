# Encapsulate Collection

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Return a protected view or copy of a collection and provide controlled modification methods.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Team {
    public List<Employee> members = new ArrayList<>();
}
```

## After: refactored code

```java
class Team {
    private final List<Employee> members = new ArrayList<>();
    public List<Employee> members() { return List.copyOf(members); }
    public void addMember(Employee employee) { members.add(employee); }
    public void removeMember(Employee employee) { members.remove(employee); }
}
```

## Why the refactoring helps

Prevents callers from bypassing collection-level rules and keeps invariants inside the owner.

## When to use it

When the collection has validation, ordering, uniqueness, or lifecycle rules.

## Cautions

Choose between an immutable snapshot and an unmodifiable live view based on the API contract.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Ensure an order cannot contain the same line item twice by controlling collection updates.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
