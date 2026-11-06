# Encapsulate Field

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Make a public field private and expose controlled access.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Account {
    public BigDecimal balance;
}
```

## After: refactored code

```java
class Account {
    private BigDecimal balance = BigDecimal.ZERO;
    public BigDecimal balance() { return balance; }
    public void deposit(BigDecimal amount) {
        if (amount.signum() <= 0) throw new IllegalArgumentException("amount must be positive");
        balance = balance.add(amount);
    }
}
```

## Why the refactoring helps

Protects invariants and prevents arbitrary callers from putting the object into an invalid state.

## When to use it

When fields are publicly mutable or callers bypass domain rules.

## Cautions

Prefer behaviour-oriented methods over a setter for every field when invariants matter.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Encapsulate a public order status field and expose valid transition methods.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
