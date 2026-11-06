# Remove Setting Method

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Remove a setter when a field should be set only at construction or through a domain operation.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Agreement {
    private final String id;
    private AgreementStatus status;
    void setId(String id) { this.id = id; }
    void setStatus(AgreementStatus status) { this.status = status; }
}
```

## After: refactored code

```java
class Agreement {
    private final String id;
    private AgreementStatus status;
    Agreement(String id) { this.id = Objects.requireNonNull(id); }
    void activate() { /* validate transition, then update */ status = AgreementStatus.ACTIVE; }
}
```

## Why the refactoring helps

Prevents arbitrary state mutation and makes valid state changes explicit.

## When to use it

When a field is immutable after creation or must change only through domain rules.

## Cautions

Frameworks and serializers may require setters; adapt construction or mapping rather than weakening invariants blindly.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Remove setStatus from Agreement and expose submit(), approve(), and terminate() transitions.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
