# Team Styles

<!-- Tocer[start]: Auto-generated, don't remove. -->

## Table of Contents

  - [Dynamics](#dynamics)
  - [Workspaces](#workspaces)
  - [Statistics](#statistics)
    - [General](#general)
    - [Software Development](#software-development)

<!-- Tocer[finish]: Auto-generated, don't remove. -->

## Dynamics

[Google learned](https://rework.withgoogle.com/blog/five-keys-to-a-successful-google-team) there are
five key dynamics that set successful teams apart from other teams:

1. **Psychological Safety**: Can we take risks on this team without feeling insecure or embarrassed?
   Team members should feel sale and able to be vulnerable in front of each other.
1. **Dependability**: Can we count on each other to do high quality work on time?
1. **Structure and Clarity**: Are goals, roles, and execution plans clear?
1. **Meaning**: Are we working on something that is personally important for each of us?
1. **Impact**: Do we fundamentally believe the work we are doing matters?

## Workspaces

- Avoid [open office design](https://is.gd/vFEBFG). It is extremely counterproductive for optimal
  software devlepment performance and happiness. Use private offices/workspaces instead. Better yet,
  avoid offices altogether and be remote-first focused. See [Distributed Employee
  Styles](distributed_employees.md) for details.

## Statistics

Make informed decisions on team performance and health by measuring the facts.

### General

- Measure current salaries against the regional/world index on a monthly basis. You want to be on
  par or higher than industry average. As part of your hiring and retention strategy, you want to
  keep evaluating this remains a qualifing factor for employee happiness.
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

### Software Development

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
