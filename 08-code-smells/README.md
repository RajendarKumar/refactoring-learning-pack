# Code Smells — Java Learning Guide

This section adds a practical Java lesson for every unique code-smell topic currently linked from Refactoring.Guru’s Code Smells navigation. Each lesson includes recognition signals, a before/after example, possible refactorings, cautions, and a practice task.

## How many smells are included?

**23 unique topics** are included here. Refactoring.Guru’s Refactoring landing page advertises “21 code smells,” while its current visible catalogue/navigation exposes 23 unique topic pages when `Incomplete Library Class` is counted once. This pack follows the linked topic catalogue so that no visible topic is omitted. The site also lists `Incomplete Library Class` under “Other Smells”; it is not duplicated in this pack.

## Category index

### Bloaters (5)
- [Long Method](01-bloaters/long-method.md)
- [Large Class](01-bloaters/large-class.md)
- [Primitive Obsession](01-bloaters/primitive-obsession.md)
- [Long Parameter List](01-bloaters/long-parameter-list.md)
- [Data Clumps](01-bloaters/data-clumps.md)

### Object-Orientation Abusers (4)
- [Switch Statements](02-object-orientation-abusers/switch-statements.md)
- [Temporary Field](02-object-orientation-abusers/temporary-field.md)
- [Refused Bequest](02-object-orientation-abusers/refused-bequest.md)
- [Alternative Classes with Different Interfaces](02-object-orientation-abusers/alternative-classes-with-different-interfaces.md)

### Change Preventers (3)
- [Divergent Change](03-change-preventers/divergent-change.md)
- [Shotgun Surgery](03-change-preventers/shotgun-surgery.md)
- [Parallel Inheritance Hierarchies](03-change-preventers/parallel-inheritance-hierarchies.md)

### Dispensables (6)
- [Comments](04-dispensables/comments.md)
- [Duplicate Code](04-dispensables/duplicate-code.md)
- [Lazy Class](04-dispensables/lazy-class.md)
- [Data Class](04-dispensables/data-class.md)
- [Dead Code](04-dispensables/dead-code.md)
- [Speculative Generality](04-dispensables/speculative-generality.md)

### Couplers (4)
- [Feature Envy](05-couplers/feature-envy.md)
- [Inappropriate Intimacy](05-couplers/inappropriate-intimacy.md)
- [Message Chains](05-couplers/message-chains.md)
- [Middle Man](05-couplers/middle-man.md)

### Other Smells (1)
- [Incomplete Library Class](06-other-smells/incomplete-library-class.md)

## Important: a smell is not an automatic instruction

- Do not refactor merely to eliminate a keyword, short method, switch, or data-only class.
- Start with the design problem: duplicated knowledge, unclear ownership, excessive coupling, hidden state, or unnecessary complexity.
- Choose a treatment proportionate to that problem. Several smells can point to the same refactoring, and one smell can have multiple valid treatments.
- Preserve behaviour with tests and small steps.

## Official references

- [Refactoring.Guru — Code Smells](https://refactoring.guru/refactoring/smells)
- [Refactoring.Guru — Catalog of Refactoring](https://refactoring.guru/refactoring/catalog)
- [Refactoring.Guru — Switch Statements](https://refactoring.guru/smells/switch-statements)