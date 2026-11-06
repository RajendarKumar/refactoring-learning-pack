# Split Temporary Variable

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Use a different variable for each logically distinct value instead of reassigning one temporary.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
double temp = 2.0;
temp = temp * item.price();
temp = temp + shippingCost;
return temp;
```

## After: refactored code

```java
double discountedUnitFactor = 2.0 * item.price();
double totalBeforeTax = discountedUnitFactor + shippingCost;
return totalBeforeTax;
```

## Why the refactoring helps

Each variable has one clear purpose and one assignment, reducing the mental burden of tracking changing meaning.

## When to use it

When one local variable is assigned more than once for unrelated stages of a calculation.

## Cautions

Do not split a variable when it represents a deliberate accumulator or loop state.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Rename and split a temporary that first stores a date and later stores a monetary amount.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
