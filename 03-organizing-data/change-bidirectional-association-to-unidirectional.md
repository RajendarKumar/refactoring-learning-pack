# Change Bidirectional Association to Unidirectional

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Remove a reverse reference when it creates unnecessary coupling or consistency work.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Department {
    private List<Employee> employees;
}
class Employee {
    private Department department;
}
```

## After: refactored code

```java
class Department {
    private List<Employee> employees;
}
class Employee {
    // Department is resolved through a repository/query when needed.
}
```

## Why the refactoring helps

Simplifies object relationships and eliminates the need to maintain two synchronized links.

## When to use it

When one direction is sufficient and reverse navigation is rarely or never needed.

## Cautions

Check query performance and persistence requirements before removing navigation.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove an unused parent pointer from a child entity and replace its use with a query.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
