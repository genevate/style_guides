# Object Oriented (OO) Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [Classes](#classes)
  - [Methods](#methods)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## Classes

- Avoid referencing instance variables directly, use getters/setters instead.
- Avoid referencing complex data structures because the structure could change.
- Super may be called when subclassing, overriding methods (especially in constructors).

## Methods

- Can expose previously hidden qualities and makes the class behavior more obvious.
- Avoid using comments. Anything that requires a comment is a candidate for refactoring into smaller
  method(s).
- Encourages code reuse, leads by example (promotes future good behavior), and keeps the code DRY.
- Makes code easier to extract/refactor to other classes and improves design.
