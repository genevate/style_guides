# CSS Styles

## General

- Avoid unclear naming conventions. A good class names should describe what it is about.
- Use the minimum number of selectors possible.
  - Yes: ul#example
  - No: #example
- Avoid descendent selectors - Requires high maintenance if the DOM heirarchy changes.
  - Yes: html div p span
- Avoid chaining selectors
  - Yes: .header.menu.actions
  - No: .header-menu-actions
- User shorthand syntax.
  - Yes:
    - padding-top: 10px;
    - padding-right: 5px;
    - padding-bottom: 1px;
    - padding-left: 2px;
  - No:
    - padding: 10px 5px 1px 2px;
- Avoid unnecessary namespacing.
  - Yes: .catalog table tr.products td.name
  - No: .catalog .products td.name
- Use link, visited, hover, and active for link styling.
- Avoid !important, use qualified selectors instead.
- Use a standard declaration order for properties:
  0. Positioning
  0. Display/Box Model
  0. Background
  0. Transitions
  0. Miscellaneous

## Media Queries

- Define media queries next to the components they modify.
- Use REM units.
- Use content-based instead of device-based breakpoints.
- Keep your styles simple by designing mobile-first.
