# Decompose Conditional

> Category: Simplifying Conditional Expressions  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Extract condition, then-branch, and else-branch logic into named methods.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
if (date.isBefore(summerStart) || date.isAfter(summerEnd)) {
    charge = quantity * winterRate;
} else {
    charge = quantity * summerRate;
}
```

## After: refactored code

```java
if (isWinter(date)) {
    charge = winterCharge(quantity);
} else {
    charge = summerCharge(quantity);
}
```

## Why the refactoring helps

Replaces date arithmetic and calculation details with business-language names.

## When to use it

When a conditional mixes a complex rule with substantial work in its branches.

## Cautions

Choose names that accurately represent the domain rule, and test boundary dates.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Decompose an agreement-validity conditional into isEffectiveOn(date) and calculateTerms().

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
