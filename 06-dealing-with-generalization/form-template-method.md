# Form Template Method

> Category: Dealing with Generalization  
> Language: Java 21 (examples use standard Java unless noted)  
## Intent

Move a common algorithm skeleton into a superclass while subclasses provide varying steps.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
class CsvImporter {
    void importFile() { open(); parseCsv(); validate(); save(); }
}
class XmlImporter {
    void importFile() { open(); parseXml(); validate(); save(); }
}
```

## After: refactored code

```java
abstract class Importer {
    final void importFile() { open(); parse(); validate(); save(); }
    protected abstract void parse();
    protected void open() { ... }
    protected void validate() { ... }
    protected void save() { ... }
}
class CsvImporter extends Importer {
    protected void parse() { parseCsv(); }
}
class XmlImporter extends Importer {
    protected void parse() { parseXml(); }
}
```

## Why the refactoring helps

Eliminates duplicated workflow structure while preserving variation points.

## When to use it

When subclasses implement the same sequence with only selected steps varying.

## Cautions

Inheritance-based hooks can be hard to compose. Consider composition when steps vary independently.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Create a common supplier import workflow with format-specific parsing.

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
