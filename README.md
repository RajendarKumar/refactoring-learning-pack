# Refactoring Learning Pack — Java Examples

A practical, example-driven companion to the Refactoring.Guru catalogue. It contains **67 individual Markdown lessons**: all 66 techniques in the Refactoring.Guru catalogue plus one additional technique from Martin Fowler's catalogue.

> The additional lesson is **Replace Loop with Pipeline**. It is included as lesson 67 for practical completeness; it is not an extra entry in the Refactoring.Guru 66-technique count.

## How to study

1. Start with `00-START-HERE.md`.
2. Read one technique at a time, preferably in catalogue order.
3. Run the examples in a small Java project and add tests before refactoring.
4. Complete the practice exercise at the end of each lesson.
5. Keep behaviour-changing work separate from refactoring commits.

## Categories

- **Composing Methods** — 9 lessons (`01-composing-methods/`)
- **Moving Features Between Objects** — 8 lessons (`02-moving-features-between-objects/`)
- **Organizing Data** — 15 lessons (`03-organizing-data/`)
- **Simplifying Conditional Expressions** — 8 lessons (`04-simplifying-conditional-expressions/`)
- **Simplifying Method Calls** — 14 lessons (`05-simplifying-method-calls/`)
- **Dealing with Generalization** — 12 lessons (`06-dealing-with-generalization/`)
- **Additional Practical Technique** — 1 lessons (`07-additional-practical-technique/`)

## Lesson index

### Composing Methods
- [Extract Method](01-composing-methods/extract-method.md)
- [Inline Method](01-composing-methods/inline-method.md)
- [Extract Variable](01-composing-methods/extract-variable.md)
- [Inline Temp](01-composing-methods/inline-temp.md)
- [Replace Temp with Query](01-composing-methods/replace-temp-with-query.md)
- [Split Temporary Variable](01-composing-methods/split-temporary-variable.md)
- [Remove Assignments to Parameters](01-composing-methods/remove-assignments-to-parameters.md)
- [Replace Method with Method Object](01-composing-methods/replace-method-with-method-object.md)
- [Substitute Algorithm](01-composing-methods/substitute-algorithm.md)

### Moving Features Between Objects
- [Move Method](02-moving-features-between-objects/move-method.md)
- [Move Field](02-moving-features-between-objects/move-field.md)
- [Extract Class](02-moving-features-between-objects/extract-class.md)
- [Inline Class](02-moving-features-between-objects/inline-class.md)
- [Hide Delegate](02-moving-features-between-objects/hide-delegate.md)
- [Remove Middle Man](02-moving-features-between-objects/remove-middle-man.md)
- [Introduce Foreign Method](02-moving-features-between-objects/introduce-foreign-method.md)
- [Introduce Local Extension](02-moving-features-between-objects/introduce-local-extension.md)

### Organizing Data
- [Change Value to Reference](03-organizing-data/change-value-to-reference.md)
- [Change Reference to Value](03-organizing-data/change-reference-to-value.md)
- [Duplicate Observed Data](03-organizing-data/duplicate-observed-data.md)
- [Self Encapsulate Field](03-organizing-data/self-encapsulate-field.md)
- [Replace Data Value with Object](03-organizing-data/replace-data-value-with-object.md)
- [Replace Array with Object](03-organizing-data/replace-array-with-object.md)
- [Change Unidirectional Association to Bidirectional](03-organizing-data/change-unidirectional-association-to-bidirectional.md)
- [Change Bidirectional Association to Unidirectional](03-organizing-data/change-bidirectional-association-to-unidirectional.md)
- [Encapsulate Field](03-organizing-data/encapsulate-field.md)
- [Encapsulate Collection](03-organizing-data/encapsulate-collection.md)
- [Replace Magic Number with Symbolic Constant](03-organizing-data/replace-magic-number-with-symbolic-constant.md)
- [Replace Type Code with Class](03-organizing-data/replace-type-code-with-class.md)
- [Replace Type Code with Subclasses](03-organizing-data/replace-type-code-with-subclasses.md)
- [Replace Type Code with State/Strategy](03-organizing-data/replace-type-code-with-state-strategy.md)
- [Replace Subclass with Fields](03-organizing-data/replace-subclass-with-fields.md)

### Simplifying Conditional Expressions
- [Consolidate Conditional Expression](04-simplifying-conditional-expressions/consolidate-conditional-expression.md)
- [Consolidate Duplicate Conditional Fragments](04-simplifying-conditional-expressions/consolidate-duplicate-conditional-fragments.md)
- [Decompose Conditional](04-simplifying-conditional-expressions/decompose-conditional.md)
- [Replace Conditional with Polymorphism](04-simplifying-conditional-expressions/replace-conditional-with-polymorphism.md)
- [Remove Control Flag](04-simplifying-conditional-expressions/remove-control-flag.md)
- [Replace Nested Conditional with Guard Clauses](04-simplifying-conditional-expressions/replace-nested-conditional-with-guard-clauses.md)
- [Introduce Null Object](04-simplifying-conditional-expressions/introduce-null-object.md)
- [Introduce Assertion](04-simplifying-conditional-expressions/introduce-assertion.md)

### Simplifying Method Calls
- [Add Parameter](05-simplifying-method-calls/add-parameter.md)
- [Remove Parameter](05-simplifying-method-calls/remove-parameter.md)
- [Rename Method](05-simplifying-method-calls/rename-method.md)
- [Separate Query from Modifier](05-simplifying-method-calls/separate-query-from-modifier.md)
- [Parameterize Method](05-simplifying-method-calls/parameterize-method.md)
- [Introduce Parameter Object](05-simplifying-method-calls/introduce-parameter-object.md)
- [Preserve Whole Object](05-simplifying-method-calls/preserve-whole-object.md)
- [Remove Setting Method](05-simplifying-method-calls/remove-setting-method.md)
- [Replace Parameter with Explicit Methods](05-simplifying-method-calls/replace-parameter-with-explicit-methods.md)
- [Replace Parameter with Method Call](05-simplifying-method-calls/replace-parameter-with-method-call.md)
- [Hide Method](05-simplifying-method-calls/hide-method.md)
- [Replace Constructor with Factory Method](05-simplifying-method-calls/replace-constructor-with-factory-method.md)
- [Replace Error Code with Exception](05-simplifying-method-calls/replace-error-code-with-exception.md)
- [Replace Exception with Test](05-simplifying-method-calls/replace-exception-with-test.md)

### Dealing with Generalization
- [Pull Up Field](06-dealing-with-generalization/pull-up-field.md)
- [Pull Up Method](06-dealing-with-generalization/pull-up-method.md)
- [Pull Up Constructor Body](06-dealing-with-generalization/pull-up-constructor-body.md)
- [Push Down Field](06-dealing-with-generalization/push-down-field.md)
- [Push Down Method](06-dealing-with-generalization/push-down-method.md)
- [Extract Subclass](06-dealing-with-generalization/extract-subclass.md)
- [Extract Superclass](06-dealing-with-generalization/extract-superclass.md)
- [Extract Interface](06-dealing-with-generalization/extract-interface.md)
- [Collapse Hierarchy](06-dealing-with-generalization/collapse-hierarchy.md)
- [Form Template Method](06-dealing-with-generalization/form-template-method.md)
- [Replace Inheritance with Delegation](06-dealing-with-generalization/replace-inheritance-with-delegation.md)
- [Replace Delegation with Inheritance](06-dealing-with-generalization/replace-delegation-with-inheritance.md)

### Additional Practical Technique
- [Replace Loop with Pipeline *(additional)*](07-additional-practical-technique/replace-loop-with-pipeline.md)

## Coverage and the 67th lesson

The Refactoring.Guru catalog page lists six technique groups. This pack includes every technique in those groups. The 67th file, `07-additional-practical-technique/replace-loop-with-pipeline.md`, is an additional technique listed in Martin Fowler's catalog and widely useful in Java collection processing.

## References

- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring Catalog](https://refactoring.com/catalog/)

## Java version and code notes

Examples target Java 21. Some snippets are intentionally partial teaching examples; comments indicate where domain types or unrelated methods are omitted. The goal is to illustrate the structural change, not to provide a complete runnable application for every lesson.
