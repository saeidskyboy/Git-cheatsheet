# Git Reference: From Beginner to Pro

A comprehensive guide to Git commands and workflows.

## Table of Contents
- [Creating & Inspecting Commits](#creating--inspecting-commits)
- [Comparing & Viewing Changes](#comparing--viewing-changes)
- [Configuration](#configuration)
- [The Staging Area](#the-staging-area)
- [Working with GitHub](#working-with-github)
- [Branches & History](#branches--history)
- [Tips & Tricks](#tips--tricks)


## Creating & Inspecting Commits

| Command                     | Description                                                                                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `git init`                  | Initializes a new Git repository in the current directory.                                                                                                               |
| `git status`                | Shows the status of files (modified, added, untracked) in the working directory and staging area.                                                                        |
| `git add <file>`            | Stages a specific file to be included in the next commit.                                                                                                                |
| `git add <folder>/`         | Stages all files within a specified folder (and its subfolders).                                                                                                         |
| `git add .`                 | Stages all files in the current directory (and its subfolders).                                                                                                          |
| `git commit -m "message"`   | Creates a new commit with the specified message.                                                                                                                         |
| `git commit --amend`        | Modifies the most recent commit, allowing you to change the commit message or add/remove staged changes.                                                                 |
| `git log`                   | Displays the commit history of the current branch.                                                                                                                       |
| `git log --oneline --graph` | Shows a compact, graphical representation of the commit history.                                                                                                         |
| `git show <commit>`         | Displays the details of a specific commit (including changes made).                                                                                                      |
| `git reflog`                | Shows a history of all actions that modified the tip of the current branch (e.g., commits, merges, rebases).                                                             |
| `git blame <file>`          | Shows who last modified each line of a file and in which commit.                                                                                                         |


## Comparing & Viewing Changes

| Command                   | Description                                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------------------- |
| `git diff`                | Shows the differences between the working directory and the staging area.                       |
| `git diff --staged`       | Shows the differences between the staging area and the last commit.                             |
| `git diff HEAD~2 HEAD`    | Shows the differences between the current commit and the commit two commits ago.                |
| `git diff branch1 branch2`| Shows the differences between two branches.                                                     |



## Configuration

| Command                                 | Description                                                                                                  |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `git config --global user.name "Name"`  | Sets your name for commits you make globally.                                                                |
| `git config --global user.email "email"`| Sets your email for commits you make globally.                                                               |


## The Staging Area (The Index)

The staging area is a buffer between your working directory and the commit history. It allows you to select which changes to include in the next commit.

| Working Directory => Staging Area | Staging Area => Commit History | Staging Area => Working Directory | Remove Changes from Working Directory  |
| --------------------------------- | ------------------------------ | --------------------------------- | -------------------------------------- |
| `git add <file>`                  | `git commit -m "message"`      | `git reset <file>`                | `git restore <file>`                   |
| `git add <folder>/`               |                                | `git reset <folder>/`             | `git restore <folder>/`                |
| `git add .`                       |                                | `git reset`                       | `git restore .`                        |

**Additional Staged Changes Commands**

| Command                       | Description                                                                                                  |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `git add -p <file>`           | Interactively choose which hunks (parts of changes) to add to the staging area.                              |
| `git mv <old> <new>`          | Moves or renames a file and stages the change.                                                               |
| `git rm --cached <file>`      | Removes a file from the staging area but keeps it in the working directory.                                  |


## Working with GitHub

| Command                                       | Description                                                                                                                                           |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git remote add origin <repository_url>`      | Adds a remote repository named "origin" with the specified URL. Typically used when cloning a repository for the first time.                          |
| `git remote -v`                               | Shows the URLs of your remote repositories.                                                                                                           |
| `git remote remove origin`                    | Removes the remote repository named "origin".                                                                                                         |
| `git push -u origin <branch_name>`            | Pushes the specified branch to the "origin" remote and sets up tracking so you can simply use `git push` in the future.                               |
| `git push --force-with-lease origin <branch>` | A safer alternative to `git push --force`, it will only push if the remote branch hasn't been updated since your last fetch.                          |
| `git pull origin <branch_name>`               | Fetches changes from the specified branch on the "origin" remote and merges them into your current branch.                                            |
| `git fetch origin`                            | Downloads all changes from the "origin" remote but doesn't merge them into your branches. Use `git merge origin/<branch>` to merge later if needed.   |


## Branches & History

| Command                            | Description                                                                                                    |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `git branch`                       | Lists all local branches.                                                                                      |
| `git branch <branch_name>`         | Creates a new branch.                                                                                          |
| `git checkout <branch_name>`       | Switches to the specified branch.                                                                              |
| `git switch -c <branch_name>`      | Creates a new branch and switches to it.                                                                       |
| `git merge <branch_name>`          | Merges the specified branch into the current branch.                                                           |
| `git rebase <branch_name>`         | Rebases the current branch onto the specified branch, creating a linear history.                               |
| `git revert <commit>`              | Creates a new commit that undoes the changes introduced by the specified commit.                               |
| `git cherry-pick <commit>`         | Applies the changes from the specified commit onto the current branch.                                         |

## Tips & Tricks

1.  **Fetch + Merge Instead of Pull:** Use `git fetch` to download changes from a remote, then `git merge origin/<branch>` to integrate them manually. This gives you more control and avoids unexpected merges.
2.  **Check Before You Push:** Always run `git pull origin <branch>` to ensure your local branch is up-to-date before pushing.
3.  **Local Bare Repositories for Practice:** Create a bare repository (`git init --bare`) to practice Git commands without affecting real projects.
4.  **Interactive Staging:** Use `git add -p` to selectively stage changes, choosing which hunks (parts of changes) to include in the next commit.
5.  **Aliases for Efficiency:** Create aliases in your `.gitconfig` file to shorten frequently used commands. For example:
    ```bash
    git config --global alias.st status
    git config --global alias.co checkout
    ```
6.  **Record and Reuse Resolutions (rerere):** Enable Git's "rerere" feature (`git config --global rerere.enabled true`) to have Git remember how you resolved merge conflicts and apply those resolutions automatically in the future. 



Let me know if you'd like any further refinements or additions to this cheat sheet! 
