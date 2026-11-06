# Inline Method

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Replace a trivial method call with its body when the method adds no useful meaning.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
int basePrice() {
    return quantity * itemPrice;
}

int price() {
    return basePrice();
}
```

## After: refactored code

```java
int price() {
    return quantity * itemPrice;
}
```

## Why the refactoring helps

Eliminates an unnecessary layer of indirection when the method name is not adding meaningful intent.

## When to use it

When a method body is as clear as its name and is not an important extension point.

## Cautions

Do not inline methods that communicate domain intent, hide complexity, or are overridden.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Find a one-line wrapper in a class and decide whether its name adds value.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
