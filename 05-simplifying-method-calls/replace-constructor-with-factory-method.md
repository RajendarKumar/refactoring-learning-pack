# Replace Constructor with Factory Method

> Category: Simplifying Method Calls  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Use a named factory method when construction requires intent, selection, or setup beyond a simple constructor.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Payment payment = new Payment("CARD", token);
```

## After: refactored code

```java
Payment payment = Payment.fromCardToken(token);
// Alternative factories can express other supported creation paths.
```

## Why the refactoring helps

Names the creation intent and can hide implementation choices.

## When to use it

When constructors are ambiguous, creation involves validation, or a subtype/implementation must be selected.

## Cautions

Do not replace every constructor mechanically; constructors are perfectly good for straightforward creation.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Replace new Payment("BANK", iban) with Payment.fromBankAccount(iban).

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
