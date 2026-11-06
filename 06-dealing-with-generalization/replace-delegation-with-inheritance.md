# Replace Delegation with Inheritance

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Use inheritance when a wrapper delegates nearly all behaviour and is truly a subtype.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class PremiumAccount {
    private Account account;
    Money balance() { return account.balance(); }
    void deposit(Money amount) { account.deposit(amount); }
    void withdraw(Money amount) { account.withdraw(amount); }
}
```

## After: refactored code

```java
class PremiumAccount extends Account {
    // Inherits the account contract and adds premium-specific behaviour.
    Money cashback() { ... }
}
```

## Why the refactoring helps

Removes needless forwarding when the wrapper genuinely satisfies the parent type contract.

## When to use it

When the delegating class is a true substitutable kind of the delegated class and needs most of its API.

## Cautions

Apply Liskov Substitution Principle: never inherit merely to save boilerplate.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Evaluate whether a specialised account really is an Account or should remain a wrapper.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
