# Separate Query from Modifier

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Split a method that returns information and changes state into a query and a command.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
BigDecimal getAndResetBalance() {
    BigDecimal result = balance;
    balance = BigDecimal.ZERO;
    return result;
}
```

## After: refactored code

```java
BigDecimal balance() { return balance; }
void resetBalance() { balance = BigDecimal.ZERO; }
```

## Why the refactoring helps

Calls become easier to reason about because reading and changing state are separate operations.

## When to use it

When a method both returns a value and has a side effect that callers may not expect.

## Cautions

If atomicity is required, expose a clearly named atomic operation rather than splitting unsafely.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Separate getAndClearFailedEvents into readFailedEvents and clearFailedEvents, preserving transaction boundaries.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
