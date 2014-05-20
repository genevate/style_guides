# Git Styles

## Clones

* For large project repositories, use the following workflow:
    0. cd (large git project)
    0. git bundle create git-bundle master
    0. mkdir new-project && cd new-project
    0. git clone (path to previously created bundle)/git-bundle -b master
    0. git remote set-url origin

## Commits

* Always write commits in past tense. This makes it easier to build and read changelogs.
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

## Pull Request Code Review Guidelines

0. No pull request should last more than a day (ideally, no more than a couple of hours).
0. Keep pull requests short, sweet, and easy to review.
0. If associated with a story, add a link in the pull request body.
0. If the pull request discussion gets noisy, stop typing and jump into a face-to-face chat. Remember: Speed and Getting
   Things Done is top priority.
0. Once reviewed, and all discussions are resolved, the reviewer must merge the feature branch into master.
0. Once reviewed and merged, the author must delete the merged branch and deploy the code to the review environment.
0. Tests must pass before a pull request can be merged. Always!
0. If, during a code review, you notice a major feature that is tangential but necessary, don't add that to the current
   workload (i.e. pull request). Create a new story for it instead and get back to resolving the pull request as
   quickly as possible.
0. In some situations, if code you are working on is specific to an environment, check in the code to a branch
   and deploy that branch to the environment while the pull request is being reviewed (review environment only).

## References

* [How to share large repositories](http://blog.plataformatec.com.br/2013/12/sharing-large-repositories-with-your-team).
