# Replace Type Code with Subclasses

> Category: Organizing Data  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Represent behaviourally different type codes with subclasses when each type needs its own behaviour.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class Employee {
    enum Type { ENGINEER, SALESPERSON }
    private Type type;
    BigDecimal bonus() {
        return type == Type.ENGINEER ? engineerBonus() : salesBonus();
    }
}
```

## After: refactored code

```java
abstract class Employee {
    abstract BigDecimal bonus();
}
final class Engineer extends Employee {
    BigDecimal bonus() { return engineerBonus(); }
}
final class Salesperson extends Employee {
    BigDecimal bonus() { return salesBonus(); }
}
```

## Why the refactoring helps

Moves type-specific behaviour into the type that owns it and avoids repeated switches.

## When to use it

When a stable type code selects genuinely different behaviour and subclasses fit the domain.

## Cautions

For simple labels with no varying behaviour, an enum is simpler. Avoid subclass explosion.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Compare an enum-based shipping calculation with separate DomesticShipping and InternationalShipping classes.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
