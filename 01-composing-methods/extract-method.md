# Extract Method

> Category: Composing Methods  
> Language: Java 21 (examples use standard Java unless noted)  
> Catalogue status: One of the 66 techniques listed in the Refactoring.Guru catalogue.

## Intent

Move a cohesive block of statements into a well-named method.

## Example scenario

Imagine a business application that manages orders, payments, suppliers, and employees. The snippet below illustrates the problem in a deliberately small example. Imports, domain declarations, and unrelated methods are omitted where they are not relevant.

## Before: code to improve

```java
void printInvoice(Invoice invoice) {
    System.out.println("Customer: " + invoice.customerName());
    System.out.println("Total: " + invoice.total());
}
```

## After: refactored code

```java
void printInvoice(Invoice invoice) {
    printInvoiceHeader(invoice);
    printInvoiceTotal(invoice);
}

private void printInvoiceHeader(Invoice invoice) {
    System.out.println("Customer: " + invoice.customerName());
}

private void printInvoiceTotal(Invoice invoice) {
    System.out.println("Total: " + invoice.total());
}
```

## Why the refactoring helps

The caller now states the high-level workflow; the extracted method names explain the details.

## When to use it

When a block has a clear purpose, can be named, or is repeated.

## Cautions

Keep the extracted method cohesive. Pass required data explicitly rather than introducing hidden shared state.

## How to apply it safely

1. Identify the current behaviour and write or run tests that capture it.
2. Make the smallest structural change that achieves this technique.
3. Run the focused unit tests, then the relevant integration tests.
4. Review edge cases, null behaviour, ordering, exceptions, and public API compatibility.
5. Commit the refactoring separately from any business-logic change.

## Practice exercise

Extract the tax calculation from an order total method into calculateTax().

## Completion checklist

- [ ] I can explain the code smell or design pressure this technique addresses.
- [ ] I can identify when this technique is useful and when it is unnecessary.
- [ ] I can apply it without changing externally observable behaviour.
- [ ] I have tests that verify the behaviour before and after the change.

## Further reading

- [Refactoring.Guru — Refactoring catalog](https://refactoring.guru/refactoring/catalog)
- [Martin Fowler — Refactoring catalog](https://refactoring.com/catalog/)
