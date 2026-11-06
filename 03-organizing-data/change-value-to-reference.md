# Change Value to Reference

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace duplicated value objects with one shared reference when identity matters.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
Customer first = new Customer("C-10", "Asha");
Customer second = new Customer("C-10", "Asha");
// Two objects represent the same real customer.
```

## After: refactored code

```java
Customer customer = customerRepository.findById("C-10");
Order first = new Order(customer);
Order second = new Order(customer);
// Both orders reference the same canonical Customer.
```

## Why the refactoring helps

Ensures one logical entity has a consistent identity and shared updates.

## When to use it

When equal-looking objects represent the same entity and identity matters across the application.

## Cautions

Use a repository/cache boundary and define identity, lifecycle, and concurrency rules.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Decide whether Address should be a value or reference and justify the identity semantics.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
