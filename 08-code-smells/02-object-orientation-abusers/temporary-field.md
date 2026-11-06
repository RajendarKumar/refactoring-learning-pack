# Code Smell: Temporary Field

**Category:** Object-Orientation Abusers  
**Language:** Java 21  
**Purpose:** Recognize the symptom, understand why it hurts, and choose a proportionate treatment.

## What is the smell?

An object has fields that are populated only during certain operations and remain meaningless or null at other times.

A code smell is a warning sign, not proof that the code is broken. Confirm the design problem before changing the implementation.

## How to recognize it

- Fields are set at the start of a method and cleared afterwards.
- Methods work only after a particular setup sequence.
- An object is unsafe to reuse concurrently because temporary state is stored on it.

## Before: a problematic design

```java
class InvoiceReport {
    private Map<String, Object> model; // only set while generate() is running

    String generate(Invoice invoice) {
        this.model = buildModel(invoice);
        String output = renderHeader() + renderLines() + renderFooter();
        this.model = null;
        return output;
    }

    private String renderHeader() { return (String) model.get("title"); }
    private String renderLines() { return model.get("lines").toString(); }
    private String renderFooter() { return "Total: " + model.get("total"); }
}
```

## After: a possible refactoring

```java
record ReportContext(String title, List<String> lines, BigDecimal total) {}

class InvoiceReport {
    String generate(Invoice invoice) {
        ReportContext context = buildContext(invoice);
        return renderHeader(context) + renderLines(context) + renderFooter(context);
    }

    private String renderHeader(ReportContext c) { return c.title(); }
    private String renderLines(ReportContext c) { return String.join("\n", c.lines()); }
    private String renderFooter(ReportContext c) { return "Total: " + c.total(); }
}
```

## Why the refactoring helps

The temporary data becomes explicit and local to one report operation. The report object no longer has a hidden lifecycle or mutable per-call state.

## Refactorings to consider

- Replace Temp with Query (when the value can be derived)
- Extract Class
- Introduce Parameter Object

These are candidate treatments, not an automatic one-to-one mapping. Pick the smallest change that addresses the actual cause.

## When not to refactor / common traps

Some fields are legitimately optional state. Focus on fields whose validity depends on a hidden sequence of calls, not every nullable field.

## Practice exercise

Find a helper class whose fields are set only during one operation. Move them to local variables or a context object passed to the methods that need them.

## Suggested safe workflow

1. Add or confirm tests for the current behaviour.
2. Make one structural change at a time.
3. Run focused tests after each change, then the full relevant suite.
4. Review API compatibility, ordering, null handling, exception behaviour, and transaction boundaries.
5. Keep the refactoring separate from unrelated feature changes.

## Reference

- [Refactoring.Guru — Temporary Field](https://refactoring.guru/refactoring/smells/oo-abusers)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)


> Examples in this pack are original Java teaching examples inspired by the concepts in the catalogue; they are not copied from the site's paid interactive course.
