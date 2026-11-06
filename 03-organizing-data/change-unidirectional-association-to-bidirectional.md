# Change Unidirectional Association to Bidirectional

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Add a reverse association when both objects need to navigate to each other.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Department {
    private List<Employee> employees;
}
class Employee {
    // No department reference.
}
```

## After: refactored code

```java
class Department {
    private final List<Employee> employees = new ArrayList<>();
    void add(Employee employee) { employees.add(employee); employee.setDepartment(this); }
}
class Employee {
    private Department department;
    void setDepartment(Department department) { this.department = department; }
}
```

## Why the refactoring helps

Allows navigation in both directions without repeatedly searching the whole collection.

## When to use it

When both sides genuinely need navigation or lifecycle coordination.

## Cautions

Keep both sides consistent in one place; watch for ORM mapping, serialization cycles, and memory retention.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Add a Supplier reference to Agreement only if agreement workflows need reverse navigation.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
