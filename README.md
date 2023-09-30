# Rebase CI Workflow Demo

One of the premise with continous integration is that all changes should _continously_ be integrated with everybody elses work. Using feature branches defets that purpouse, as the feature branch will be out of sync with the main branch. With feature branches you hide code from everybody else. Instead of using feature branches, it is better to use the concept of _feature flags_ to hide the feature until it is ready to be used. Partly done features and changes will get released into production, and that is fine.

However, when working localy on bigger refactoring it is convenient to at least be able to do a couple of commits on a local "feature" branch. This branch should **not** be pushed, but merged into main at least daily. It is solely used to make it easier to work with the code locally.

## Workflow

The workflow is as follows:

1. Create a feature branch from the main branch but **do not** push it to the remote repository. It is only used locally and should have an extreme short life span, at most a day.
2. Do your work on the feature branch and commit as often as you like.
3. When you are done, rebase the main branch onto the feature branch. This will make it look like you did all your work on the main branch.
4. Push the main branch to the remote repository.
