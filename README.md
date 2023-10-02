# Rebase CI Workflow Demo

One of the premise with continous integration is that all changes should _continously_ be integrated with everybody elses work. Using feature branches defets that purpouse, as the feature branch will quickly be out of sync with the main branch. With feature branches you hide code from everybody else. Instead of using feature branches, it is better to use the concept of _feature flags_ to disable the feature until it is ready to be used. Partly done features and changes will get released into production, and that is fine.

However, when working localy on bigger refactoring it is convenient to at least be able to do a couple of commits on a local "feature" branch. This branch should **not** be pushed, but merged into main at least daily. It is solely used to make it easier to work with the code locally.

## Workflow

The workflow is as follows:

1. Create a feature branch from the main branch. It is only used locally and should have an extreme short life span, at most a day.
2. Do your work on the feature branch and commit as often as you like.
3. When you are done, rebase the main branch onto the feature branch. This will make it look like you did all your work on the main branch.
4. Push the main branch to the remote repository.

## GitHub CI repo settings

GitHub has various features to help with keeping the main branch in a good state. The following settings are recommended:

- [Require status checks before merging](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging)
- [Require branches to be up to date before merging](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-branches-to-be-up-to-date-before-merging)
- [Include administrators](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#include-administrators)

## Avoid merge commits

If you want to avoid merge commits, you can use the [_Require linear history_](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-linear-history) setting in GitHub. This setting is a mather of preferences.

## Require status checks before merging

The [_Require status checks before merging_](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-before-merging) setting in GitHub is a great way to reduce the chance of breaking the main branch. Be sure to include the GitHub CI workflow in the list of required status checks.

## Require status checks to pass before merging

With the [_Require status checks to pass before merging_](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches#require-status-checks-to-pass-before-merging) setting in GitHub you can require that all status checks must pass before a pull request can be merged. This is a great way to reduce the chance of breaking the main branch. The checks are done in a seperate branch.
