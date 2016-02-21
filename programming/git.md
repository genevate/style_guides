# Git Styles

## General

- Avoid checking in development-specific configuration files (add to .gitignore instead).
- Avoid checking in sensitive information (i.e. security keys, passphrases, etc).
- Avoid using "WIP" (a.k.a. "Work in Progress") commits and/or pull requests. Be confident with your code and collegues'
  time. Use branches, stashes, etc. instead -- share a link to a diff if you have questions/concerns during development.

## Commits

- Use small, atomic commits:
  - Easier to document with detailed subject messages (especially when grouped together in a pull request).
  - Easier to reword, edit, squash, fix, and drop when interactively rebasing.
  - Easier to merge together versus tearing apart larger commits.
- Use the following format for the first line of the commit message:
  - Use 50 characters or less.
  - Use past tense (makes it easier to build and read release notes).
  - Use the following prefixes only:
    - *Fixed* - Existing code that has been fixed.
    - *Removed* - Code that was once added and is now removed.
    - *Added* - New code that is an enhancement, feature, etc.
    - *Updated* - Existing code that has been updated.
    - *Refactored* - Existing code that has been refactored.
  - Use hashtags (easier to search for later).
- Use the following format for the body of the commit message:
  - Use a space between the first line of the commit message and the body.
  - Use a bullet for each detail of the commit body.
  - Include links to dependent projects, stories, etc. if available (usually the first bullet point).
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

## Pull Requests

- Avoid authoring and reviewing your own pull request.
- Review and merge pull requests quickly:
  - Maintain a consistent pace -- Review morning, noon, and night.
  - Try not to let them linger more than a day.
- Keep pull requests short and easy to review:
  - Provide a high level overview that answers *why* this pull request is necessary.
  - Provide a link to the story/task that prompted the pull request.
  - Provide screenshots/screencasts if possible.
  - Ensure all commits within the pull request are related to the purpose of the pull request.
- If the pull request discussion gets noisy, stop typing and switch to face-to-face chat.
- If during a code review, additional features are discovered, create stories for them and then return to reviewing the
  pull request.
- The author, not the reviewer, should merge the feature branch upon approval.
- Ensure the following criteria is met before merging your feature branch to master:
  - Ensure all *fixup!* and *squash!* commits are interactively rebased and merged.
  - Ensure your feature branch is rebased upon `master`.
  - Ensure all tests are passing.
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
