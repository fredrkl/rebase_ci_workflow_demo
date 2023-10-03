# Rebase CI Workflow Demo

One of the premise with continuous integration is that all changes should _continuously_ be integrated with everybody else's work. Using feature branches defeats that purpose, as the feature branch will quickly be out of sync with the main branch. With feature branches you hide code from everybody else. Instead of using feature branches, it is better to use the concept of _feature flags_ to disable the feature until it is ready to be used. Partly done features and changes will get released into production, and that is fine.

However, when working locally on bigger refactoring it is convenient to at least be able to do a couple of commits on a local "feature" branch. This branch should be merged into main **at least** daily. It is solely used to make it easier to work with the code locally.

## Workflow

The workflow is as follows:

1. Create a branch from the main branch. It should have an extremely short life span, at most a day.
2. Do your work on the branch and commit as often as you like.
3. When you are done, rebase the main branch onto the branch. This will make it look like you did all your work on the main branch.
4. Push the main branch to the remote repository.

## GitHub CI repo settings

GitHub has various features to help with keeping the main branch in a good state. The following settings are recommended:

- [Avoid merge commits](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-linear-history)
- [Require status checks before merging](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging)
- [Include administrators](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#include-administrators)

## Avoid merge commits

If you want to avoid merge commits, you can use the [_Require linear history_](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-linear-history) setting in GitHub. This setting is a matter of preferences, and it is not required for this workflow to work. However, it can be a good idea to avoid merge commits, as they can make the history harder to read.

## Require status checks before merging

One way to avoid constantly breaking the main branch, without using feature branches and _pull requests_, is the [_Require status checks before merging_](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging) setting in GitHub. With this setting you will need to verify the git SHA by running the listed GitHub CI workflow checks another branch before pushing to main.

## Example

Using this repo as an example. We have a main branch and a _build check_ using _GH Actions_ located in the .github/workflows folder. I have enabled the following features on the _main_ branch:

- Require status checks before merging
- Require linear history
- Do not allow bypassing the above settings

I create a branch and start working on a feature. I do a couple of commits and push the branch to the remote repo. As soon as the branch builds I do a rebase of the main branch onto my feature branch. This will make it look like I did all my work on the main branch. I then push the main branch to the remote repo. In a sense the branch is used to verify checks and gather feedback before pushing to main. If you do not need the checks, you can skip pushing the branch to the remote repo and just rebase the main branch locally. Or you can simply commit to the main branch directly and push.

## FAQ

### Why not just create a branch and a PR?

A branch hides and stops the work from being integrated with everybody else's work. It is also overhead to create a PR for every small change, and can potentially stop everybody else's flow when they constantly have to approve PRs. The PR will also be out of sync with the main branch very quickly, and it will be hard to merge it into the main branch.

If everyone is working on their own branch and not continuously integrate into the main branch it does not matter if everyone else is merging main into their branch.

### What about verifying multiple reviewers?

In certain cases it can be a good idea to have multiple reviewers and pull requests to prove to reviewers that multiple reviewers, e.g, PCI-DSS compliance.

### What about controlling design decisions?

Having a reviewer for all pull requests to control design decisions is a bad idea. That person quickly becomes a bottleneck and the project slows down. Instead, you should have design sessions before starting on issues and do pair programming.
