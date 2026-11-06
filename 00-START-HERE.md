# Start Here: Learning Refactoring with Java

## What refactoring means

Refactoring is a disciplined change to the internal structure of code that preserves its externally observable behaviour. It is not a feature change, bug fix, or wholesale rewrite.

## The safe refactoring loop

1. **Establish behaviour.** Read the code and add characterization/unit tests where needed.
2. **Choose one technique.** Name the problem first; do not refactor just to apply a pattern.
3. **Make a small change.** Prefer IDE-assisted transformations for rename, extract method, move method, and similar mechanical operations.
4. **Run tests immediately.** Start with focused tests, then broader integration tests.
5. **Review the diff.** Look for accidental behaviour changes, API changes, transaction changes, altered ordering, or new coupling.
6. **Commit separately.** Keep refactoring separate from feature work so rollback and review remain easy.

## Code Smells: learn to recognize the reason before choosing a fix

A **code smell** is a symptom; a **refactoring technique** is a transformation you may apply to address it. One smell can have several treatments, and the right treatment depends on the cause. For example, a complex switch can sometimes be replaced with polymorphism, but a small stable switch can remain as-is.

Read [08-code-smells/README.md](08-code-smells/README.md) for 23 individual smell lessons with Java examples. A useful first topic is [Switch Statements](08-code-smells/02-object-orientation-abusers/switch-statements.md).

## A suggested learning sequence

- **Beginner:** Extract Method, Rename Method, Extract Variable, Replace Magic Number with Symbolic Constant, Replace Nested Conditional with Guard Clauses, Encapsulate Field.
- **Intermediate:** Move Method, Extract Class, Introduce Parameter Object, Replace Primitive with Object, Replace Conditional with Polymorphism, Separate Query from Modifier.
- **Advanced:** Replace Method with Method Object, Change Value to Reference, Change Bidirectional Association to Unidirectional, Form Template Method, Replace Inheritance with Delegation.

## Important distinctions

- **Refactoring vs. feature change:** first restructure while preserving behaviour; then add the feature in a separate change.
- **Code smell vs. refactoring:** a smell is a symptom; a refactoring is one possible treatment.
- **Pattern vs. refactoring:** a pattern is a reusable design; a refactoring is a transformation from one code structure to another.
- **Do not over-refactor:** a technique is useful only when it makes the code easier to understand or change.

## Practice rule

For each lesson, explain the intent in your own words, reproduce the before/after transformation, write tests for the behaviour, and complete the exercise. Refactoring skill comes from repeated, test-backed practice.

See [README.md](README.md) for the complete 90-lesson index, including Code Smells.
