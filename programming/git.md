# Git Styles

## General

- Avoid checking in development-specific configuration files (add to `.gitignore` instead).
- Avoid checking in sensitive information (i.e. security keys, passphrases, etc).
- Avoid "WIP" (a.k.a. "Work in Progress") commits and/or pull requests. Be confident with your code
  and collegues' time. Use branches, stashes, etc. instead -- share a link to a diff if you have
  questions/concerns during development.

## Commits

- Use small, atomic commits:
  - Easier to document with detailed subject messages (especially when grouped together in a pull
    request).
  - Easier to reword, edit, squash, fix, or drop when interactively rebasing.
  - Easier to merge together versus tearing apart larger commits.
- Use the following format for the first line of the commit message:
  - Use 50 characters or less.
  - Use past tense (makes it easier to build and read release notes).
  - Use the following prefixes only:
    - *Fixed* - Existing code that has been fixed.
    - *Removed* - Code that was once added and is now removed.
    - *Added* - New code that is an enhancement, feature, etc.
    - *Updated* - Existing code that has been modified.
    - *Refactored* - Existing code that has been refactored and does not change functionality.
  - Use hashtags to identify code (easier to search for later).
- Use the following format for the body of the commit message:
  - Use a space between the first line of the commit message and the body.
  - Use a bullet for each detail of the commit body.
  - Include links to dependent projects, stories, etc. if available.
- Each commit message should answer the following:
  - Why? -- Why is the body of work necessary?
  - What? -- What is the body of work being committed.
  - How? -- How does the body of work solve the why.

## Branches

- Always work in feature branches.
- Always maintain feature branches by rebasing upon `master` on a regular basis.

## Tags

- Always tag your releases:
  - Makes it easier to record milestones and capture associated release notes.
  - Makes it easier to compare differences between versions.
  - Makes adoption of the new changes easier and faster.

## Rebases

- Avoid rebasing a shared branch. If you must do this, clear communcation should be used to warn
  those ahead of time, ensure that all of their work is checked in, and that their local branch is
  deleted first.

## Pull Requests

- Avoid authoring and reviewing your own pull request.
- Keep pull requests short and easy to review:
  - Provide a high level overview that answers *why* the pull request is necessary.
  - Provide a link to the story/task that prompted the pull request.
  - Provide screenshots/screencasts if possible.
  - Ensure all commits within the pull request are related to the purpose of the pull request.
- Review and merge pull requests quickly:
  - Maintain a consistent pace -- Review morning, noon, and night.
  - Try not to let them linger more than a day.
- Use emojis to help identify the types of comments added during the review process:
  - Generally, an emoji should prefix all feedback. Format: `<emoji> <feedback>`.
  - :tea: - Signifies you are reviewing the pull request. This is *non-blocking* and is meant to be
    informational. Useful when reading over a pull request with a large number of commits, reviewing
    complex code, requires additional testing by the reviewer, etc.
  - :information_source: - Signifies informational feedback that is *non-blocking*. Can also be used
    to let one know you are done reviewing but haven't approved yet (due to feedback that needs
    addressing), rebasing a pull request and then merging, waiting for a blocking pull request to be
    resolved, status updates to the pull request, etc.
  - :art: - Signifies an issue with code style and/or code quality. This can be *blocking* or *non-
    blocking* feedback but is feedback generally related to the style/quality of the code,
    implementation details, and/or alternate solutions worth considering.
  - :bulb: - Indicates a helpful tip or trick for improving the code. This can be *blocking* or
    *non-blocking* feedback and is left up to the author to decide (generally, it is a good idea to
    address and resolve the feedback).
  - :star: - Signifies code that is liked, favorited, remarkable, etc. This feedback is *non-
    blocking* and is always meant as positive/uplifting.
  - :white_check_mark: - Signifies approval of a pull request. The author can merge to `master` and
    delete the feature branch at this point.
- If the pull request discussion gets noisy, stop typing and switch to face-to-face chat.
- If during a code review, additional features are discovered, create stories for them and then
  return to reviewing the pull request.
- The author, not the reviewer, should merge the feature branch upon approval.
- Ensure the following criteria is met before merging your feature branch to master:
  - Ensure all *fixup!* and *squash!* commits are interactively rebased and merged.
  - Ensure your feature branch is rebased upon `master`.
  - Ensure all tests and code quality checks are passing.
  - Ensure the feature branch is deleted after being successfully merged.

## Archives

- For large project repositories, use the following workflow:
  0. cd (large git project)
  0. git bundle create git-bundle master
  0. mkdir new-project && cd new-project
  0. git clone (path to previously created bundle)/git-bundle -b master
  0. git remote set-url origin

## References

- [How to share large repositories](http://blog.plataformatec.com.br/2013/12/sharing-large-repositories-with-your-team).
