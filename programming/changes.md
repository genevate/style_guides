# Changes Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [Overview](#overview)
  - [General](#general)
  - [Resources](#resources)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## Overview

Keeping a history of changes for software projects is extremely important in communicating the
evoluation of a project over time to new contributors to a project.

## General

- Use human readable text, always. If you link to a commit SHA, for example, give it a proper
  label/description. All changes are meant for human consumption and should be written that way.
- Use a consistent date/time format for all version releases. Example: `2018-09-15`.
- Use bullet points for each detail of each version release. Example:

      # 1.0.0 (2018-09-15)

      - Fixed...
      - Added...
      - Updated...
      - Removed...
      - Refactored...
- Use a sorted list of version releases with the most recent release at the top followed by previous
  releases.
- Use version releases where each category of details is grouped together. Example:

      # 1.0.0 (2018-09-15)

      - Fixed one...
      - Fixed two...
      - Fixed three...
      - Added...
      - Updated one...
      - Updated two...
      - Removed one...
      - Removed two...
      - Refactored...
- Use consistently structured version releases. As shown above, the format and structure of each
  version release should be identical.
- Use only public API relevant information in building up version release changes.

## Resources

- [Keep a Changelog](https://keepachangelog.com) - An example of what a history of changes could
  look like.
