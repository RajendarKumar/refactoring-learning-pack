# Replace Error Code with Exception

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Use exceptions to represent exceptional failure instead of returning magic error codes.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
int loadSupplier(String id) {
    if (!repository.exists(id)) return -1;
    return 0;
}
```

## After: refactored code

```java
void loadSupplier(String id) {
    if (!repository.exists(id)) {
        throw new SupplierNotFoundException(id);
    }
}
```

## Why the refactoring helps

Uses the language’s error channel and prevents callers from accidentally ignoring failure codes.

## When to use it

When failure is exceptional and a return value is otherwise needed for normal results.

## Cautions

Do not use exceptions for ordinary branching. Define meaningful exception types and document recovery behaviour.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace a negative return code from agreement lookup with AgreementNotFoundException.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
