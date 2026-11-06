# Code Smell: Switch Statements

**Category:** Object-Orientation Abusers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

A complex switch or repeated if/else chain selects behaviour based on a type or state. The same decision may be duplicated in multiple places.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- A new type requires editing several switch statements.
- Each branch contains substantial, type-specific behaviour.
- The same enum or type code is checked across unrelated services.

## Before: a problematic design

```java
enum DeliveryType { STANDARD, EXPRESS, OVERNIGHT }

class DeliveryCostCalculator {
    BigDecimal calculate(DeliveryType type, BigDecimal weight) {
        return switch (type) {
            case STANDARD  -> weight.multiply(new BigDecimal("1.00"));
            case EXPRESS   -> weight.multiply(new BigDecimal("1.75"));
            case OVERNIGHT -> weight.multiply(new BigDecimal("2.50"));
        };
    }
}
```

## After: a possible refactoring

```java
@FunctionalInterface
interface DeliveryPolicy {
    BigDecimal costFor(BigDecimal weight);
}

class DeliveryCostCalculator {
    private final Map<DeliveryType, DeliveryPolicy> policies = Map.of(
        DeliveryType.STANDARD,  w -> w.multiply(new BigDecimal("1.00")),
        DeliveryType.EXPRESS,   w -> w.multiply(new BigDecimal("1.75")),
        DeliveryType.OVERNIGHT, w -> w.multiply(new BigDecimal("2.50"))
    );

    BigDecimal calculate(DeliveryType type, BigDecimal weight) {
        DeliveryPolicy policy = policies.get(type);
        if (policy == null) throw new IllegalArgumentException("Unsupported delivery type: " + type);
        return policy.costFor(weight);
    }
}
```

## Why the refactoring helps

The decision is represented as a strategy registry. In a larger system, each policy can be a separate implementation injected by Spring, allowing policy-specific behaviour to evolve independently.

## Refactorings to consider

- Replace Conditional with Polymorphism
- Replace Type Code with Subclasses
- Replace Type Code with State/Strategy
- Replace Parameter with Explicit Methods
- Introduce Null Object (for a meaningful null case)

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

A switch is not automatically a smell. Keep a small, stable switch when it is clearer, such as a simple enum-to-label mapping or a factory selection. Polymorphism is most useful when branches contain distinct behaviour or the same decision is repeated.

## Practice exercise

Find a switch that calculates fees or selects a workflow. Check whether the same type is switched on elsewhere. Refactor only if each branch owns meaningful behaviour; otherwise keep the switch simple.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Switch Statements](https://refactoring.guru/smells/switch-statements)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)

## Refactoring.Guru's specific guidance

Refactoring.Guru recommends first locating the switch in the class that owns the behaviour, then considering type-code replacement and Replace Conditional with Polymorphism. It explicitly says simple switches and factory-selection switches can be left alone.


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
