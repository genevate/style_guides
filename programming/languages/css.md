# CSS Styles

- Avoid unclear naming conventions. A good class names should describe what it is about.
- Use the minimum number of selectors possible.
  - Bad: ul#example
  - Good: #example
- Avoid descendent selectors - Requires high maintenance if the DOM heirarchy changes.
  - Bad: html div p span
- Avoid chaining selectors
  - Bad: .header.menu.actions
  - Good: .header-menu-actions
- User shorthand syntax.
  - Bad:
    - padding-top: 10px;
    - padding-right: 5px;
    - padding-bottom: 1px;
    - padding-left: 2px;
  - Good:
    - padding: 10px 5px 1px 2px;
- Avoid unnecessary namespacing.
  - Bad: .catalog table tr.products td.name
  - Good: .catalog .products td.name
- Use link, visited, hover, and active for link styling.
- Avoid !important, use qualified selectors instead.
- Use a standard declaration order for properties:
  0. Positioning
  0. Display/Box Model
  0. Background
  0. Transitions
  0. Miscellaneous
