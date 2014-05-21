# Git Styles

## General

* Avoid checking in development-specific configuration files (add to .gitignore instead).
* Avoid checking in sensitive information (i.e. security keys, passphrases, etc).

## Clones

* For large project repositories, use the following workflow:
    0. cd (large git project)
    0. git bundle create git-bundle master
    0. mkdir new-project && cd new-project
    0. git clone (path to previously created bundle)/git-bundle -b master
    0. git remote set-url origin

## Commits

* Always write commits in past tense (makes it easier to build and read changelogs).
* Always prefix commits using one of the following:
    * **Fixed** - This is code that has been fixed.
    * **Removed** - This is a feature that was once added but is now removed.
    * **Added** - This is a new feature.
    * **Updated** - This is an existing feature that has been updated.
    * **Refactored** - This is a code that has been refactored.
* Use hashtags in commit messages if helpful. These can easily be searched for later.
* Use the --message option for short one-line commit messages sparingly. Better to use a short one-line commit message
  but also provide bullet points, within the commit message body, which detail and support the one-line commit message.
* Include links (via the commit message body, usually) to dependent projects, etc. if useful.

## Tags

* Always tag your releases.
    * Makes it easier to build changelogs.
    * Makes it easier to compare differences between versions.
    * Makes adoption of the new changes easier and faster.

## Pull Requests

* Avoid authoring and reviewing your own pull request.
* Review and merge pull requests quickly (ideally, don't let them linger more than a couple of hours max).
* Keep pull requests short, sweet, and easy to review.
* Add story links to pull request message bodies (if applicable).
* If the pull request discussion gets noisy, stop typing and switch to face-to-face chat.
* Once reviewed and discussions resolved, the reviewer should merge the feature branch.
* As a reviewer, ensure all tests pass before merging.
* Once reviewed and merged, the author should delete the merged branch (local and remote).
* If during a code review, additional features are discovered, create stories for them and then return to reviewing the
  pull request.
* In some situations, if the code you are working on is specific to an environment, check in the code to a branch
  and deploy that branch to the environment while the pull request is being reviewed (review environment only).

## Workflows

### Basic Workflow (common to all workflows)

0. Pull down latest code for master or feature branch.
0. Use `git commit --message` to commit small/readable changes and add commit comments.
0. Use `git pull --rebase` to put local commits on top of upstream changes.
0. Use `git push` to commit small/readable changes as work progresses.

### Local Soloist -- Local Reviewer

0. Commit and rebase.
0. Review changes with teammate when ready to push to remote: `git diff origin/master`.
0. Use interactive rebase (`git rebase -i @{u}`) to clean up commits, commit messages, etc. one last time before
   pusing to remote. CAUTION: This rewrites history so don't do this for commits you don't own or have already pushed
   remotely.

### Local/Remote Soloist -- Remote Reviewer

0. Create a feature branch.
0. Commit changes.
0. Issue a GitHub pull request once all commits for work is complete and ready for review.
0. While waiting for pull request to be accepted, start new work on another feature branch.

### Local/Remote Pairs

In this situation, two people are sharing the same screen and codebase together (either local or remote). There is no
need to create a branch or issue pull requests since the pairs are communicating in realtime. This workflow is the same
as the basic workflow mentioned above.

## References

* [How to share large repositories](http://blog.plataformatec.com.br/2013/12/sharing-large-repositories-with-your-team).
