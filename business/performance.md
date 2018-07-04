# Performance Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [Personnel](#personnel)
  - [Engineering](#engineering)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## Personnel

- Measure current salaries against a regional/world index on a monthly basis. You want to be on par
  or higher than industry average. As part of your hiring and retention strategy, you want to keep
  evaluating this remains a qualifing factor for employee happiness.
- Measure voluntary and involuntary departures from the company. It's important to know and
  understand the reasons why people leave and make adjustments based on their feedback.
- Measure, evaluate, and refine the interviewing process for each candidate based on their feedback
  and current state of the company.
- Measure the onboarding experience to ensure time to productivity is low. Idealy, a new hire on the
  first day should be fully setup within the system (i.e. paperwork completed), development
  environment setup, new code checked in, and changes deployed to production.
- Measure the ratio of managers to contributors. Ideally, this would be one manager to five
  contributors. Max is one manager to ten contributors. Anything more than the max and you risk team
  retention and happiness.

## Engineering

Rather than spend time on story pointing or arbitrary guesswork and estimation, focus on what you
can measure. These metrics help provide insight on the speed in which code is shipped. The following
should be evaluated on a weekly basis:

  - Number of pull requests opened.
  - Number of pull requests rebased.
  - Number of comments per pull request. Too high a number might mean any or all of the following:
    - Poor design and planning.
    - Poor team rapport/communication.
    - Lack of code quality automation (i.e. linters, automated builds, etc.)
  - Average time to rebase (i.e. the number of pull requests rebased under a specific threshold).
  - Number of production deploys.
  - Number of bugs. Ideally, this should remain zero and always be top priority. If it increases
    over time, you have a quality control problem.
