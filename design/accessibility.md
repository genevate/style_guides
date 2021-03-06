# Accessibility Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [General](#general)
  - [Checklists](#checklists)
  - [Guidelines](#guidelines)
  - [Tools](#tools)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## General

- [Web Accessibility Business Case](https://www.w3.org/WAI/bcase/Overview) - Reason why it is
  important to design with accessibility in mind.
- [Web Accessibility Fundamentals](https://www.w3.org/WAI/fundamentals/accessibility-intro) - Learn
  the fundamentals (especially how people with disabilities use the web).
- [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21) - These are the
  official W3C recommendations.
- [WAI-ARIA Authoring Practices](http://w3c.github.io/aria-practices) - Provides information on how
  to use WAI-ARIA properly within rich web applications.
- [Designing for Accessibility](https://is.gd/T3eZCD) - It doesn't need to be hard to design for
  accessibility. This article walks through the core criteria.
- [Accessibility Developer Guide](https://www.accessibility-developer-guide.com) - A getting started
  guide to accessible web development.
- [A11Y Style Guide](https://a11y-style-guide.com/style-guide) - A living document with examples and
  code snippets.

## Checklists

- [Accessibility Guidelines](http://accessibility.voxmedia.com) - A master checklist for designers,
  engineers, project managers, quality assurance, and editorial staff to follow.

## Guidelines

- Use semantic structure as it is more important than developer ergonomics.
- Use `lang` attribute to ensure document is read correctly via screen readers. Common use is `<html
  lang="en-US">` but can also be applied to specific tags within the document when content contains
  mixed use of language.
- Use concise but descriptive text for image `alt` attributes. Example: *"Red barn with aluminum
  roof and dilapidated wooden door set against freshly plowed field and clear blue sky."*
- Use the image `alt` attribute to avoid invalid HTML and inconsistent behavior. It also prevents
  the screen reader from reading from the `src` attribute when the `alt` attribute is missing.
- Use the same embedded image text for `alt` attributes.
- Use an empty `alt` attribute when an image doesn't add valuable content, is adjacent to related
  text content, or is considered a decorative image.
- Use [W3C's Image alt Decission Tree](https://www.w3.org/WAI/tutorials/images/decision-tree).
- Use proper punctuation when writing text that will be read by screen readers to be more
  converstational sounding.
    - Use commas to provide a short break while announcing content.
    - Use periods at the end of each sentence to cause the screen reader to pause for a moment
      before continuing.
- Avoid the  `title` attribute as it has [limited
  value](https://developer.paciellogroup.com/blog/2010/11/using-the-html-title-attribute) on mobile
  devices, touch screens, screen readers, etc. Consider displaying the text as part of your design
  rather than relying on it automatically showing up.
- Avoid the `placeholder` attribute (or if used, ensure it ends up being a label so valuable
  usage information isn't lost).
- [Avoid default field validation](http://adrianroselli.com/2019/02/avoid-default-field-validation.html)
  as it is harmful to accessibility.
- [Avoid `aria-roledescription`
  property](https://adrianroselli.com/2020/04/avoid-aria-roledescription.html) because it tends to
  be misused which causes confusion for screen readers more often than not.
- [Avoid opening links in new windows/tabs](https://adrianroselli.com/2020/02/link-targets-and-3-2-5.html).

## Tools

- [aXe](https://www.axe-core.org) - An accessibility engine for testing the quality of your design.
- [Contrast](https://usecontrast.com) - A macOS app for detecting low quality contrast in your
  design.
- [Lighthouse](https://developers.google.com/web/tools/lighthouse) - A code quality tool for web
  apps. Provides performance, progressive web app, accessibility, best practices, and SEO scores. It
  can be installed as a Chrome extension, CLI, or Node module. Pro
