# Git Reference: From Beginner to Pro

A comprehensive guide to Git commands and workflows.

## References & Resources

* **Hidden Git Commands:**  Scott Chacon (GitHub Co-founder) - [YouTube Video](https://www.youtube.com/watch?v=aolI_Rz0ZqY&list=WL&index=8)
* **GitHub Crash Course for Beginners (2024):** Cameron McKenzie - [YouTube Video](https://www.youtube.com/watch?v=l2yrJtwoC_E)
* **How to Undo Mistakes with Git:** Tobias Günther - [YouTube Video](https://www.youtube.com/watch?v=lX9hsdsAeTk)
* **Official Git Documentation:** [https://git-scm.com/docs](https://git-scm.com/docs)


## Table of Contents
- [Creating & Inspecting Commits](#creating--inspecting-commits)
- [Comparing & Viewing Changes](#comparing--viewing-changes)
- [Configuration](#configuration)
- [The Staging Area](#the-staging-area)
- [Working with GitHub](#working-with-github)
- [Undo Mistakes with Git (Like a Pro)](#undo-mistakes-with-git-like-a-pro)
- [Branches & History](#branches--history)
- [Advanced Commit Manipulation](#advanced-commit-manipulation)
- [Working with Remotes](#working-with-remotes)
- [Additional Tools & Tips](#additional-tools--tips)

## 🚨 Houston, We Have a Commit History! 🚨

Below are tools for rewriting history, BUT remember the golden rule of Git:

**NEVER rewrite a commit history that has already been pushed to a remote repository (unless you want to be the subject of office memes).**

- `--amend`
- `Rebase`
- `Interactive rebase`
- `reset`

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
| `git log -a --decorate --oneline --graph` | Visualizes your commit history as a beautiful ASCII graph. Perfect for understanding branch merges, rebases, and the overall flow of your project.         |
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


## Undo Mistakes with Git (Like a Pro)

Git provides a powerful toolkit for fixing mistakes. Here's how to handle common scenarios:

### Understanding the Basics

* **Hunks and Chunks:**
    - **Hunk:** A section of code that's been changed within a file (like a paragraph).
    - **Chunk:** A smaller piece of a hunk (like a sentence).
* **Inspecting Changes:** Always start by using `git diff <file>` to see the differences between versions before undoing anything.

### Discarding Uncommitted Changes

* **Restore a Single File:** `git restore <file>` (**Caution:** This is irreversible!)
* **Restore a Deleted File (Before Committing):** `git restore <file>`
* **Discard Part of a File's Changes:** `git restore -p <file>` (Interactively select hunks/chunks to discard)
* **Discard All Uncommitted Changes:** `git restore .` (**Caution:** This affects all files!)

### Modifying Existing Commits

* **Amend Last Commit:** `git commit --amend -m "New message"` (Changes message or content of the most recent commit. Avoid using on pushed commits.)
* **Revert a Specific Commit:** `git revert <commit_id>` (Creates a new commit that undoes the changes of the specified commit. Safe for pushed commits.)

### Resetting to an Older State (Use with Caution!)

* **Resetting the Entire Branch:**
    - `git reset --hard <commit_id>`: Discards all changes made after the specified commit. (**Caution:** Can cause data loss!)
    - `git reset --mixed <commit_id>`: Keeps changes made after the specified commit but unstages them.
* **Resetting a Single File:**
    - `git log <file>`: Find the commit ID you want to revert to.
    - `git restore --source=<commit_id> <file>`: Restores the file to the state it was in at that commit.

### Fixing Pushed Mistakes

* **Creating a New Branch from a Mistaken Commit:**
    - `git branch <new_branch_name> <mistaken_commit_id>`
* **Removing the Commit from the Original Branch:**
    - `git reset HEAD~1 --hard` (Only if the mistaken commit is the most recent one)
* **Moving a Commit to a Different Branch (Cherry-Picking):**
    - `git checkout <target_branch>`
    - `git cherry-pick <commit_id>` 

### Interactive Rebase (Advanced)

* **Rewriting Commit History:** `git rebase -i <commit_id>` (Allows for editing, squashing, reordering, or dropping commits. Avoid on pushed commits!)
* **Fixing Previous Commits:**
    - Make your changes.
    - `git add <changed_files>`
    - `git commit --fixup=<commit_id_to_fix>`
    - `git rebase -i --autosquash <base_commit>` (Squashes the fixup commit into the original)

**Important Note:** Rewriting commit history (with `--amend`, `rebase`, `interactive rebase`, or `reset`) on commits that have been pushed to a shared repository can cause serious problems for your collaborators. Use these commands with caution!


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

## Advanced Commit Manipulation

| Command                                       | Description                                                                                                                                                                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git commit -m "message" --amend`             | Modifies the most recent commit's message or staged changes.                                                                                                                                                              |
| `git revert <commit>`                         | Creates a new commit that undoes the changes made in a specific commit. This is a safer way to undo changes than resetting, as it doesn't alter the existing commit history.                                              |
| `git reset --hard <commit>`                   | Resets the current branch to a specified commit, discarding all changes made after that commit. This should be used with caution, as it can result in data loss.                                                          |
| `git reset --mixed <commit>`                  | Resets the current branch to a specified commit, but keeps the changes made after that commit in the working directory (unstages them). This is the default behavior of `git reset`.                                      |
| `git cherry-pick <commit>`                    | Applies the changes from a specific commit onto the current branch. Useful for selectively applying changes from other branches.                                                                                          |
| `git rebase -i <commit>`                      | Starts an interactive rebase, allowing you to modify, combine, or reorder commits.                                                                                                                                        |
| `git commit --fixup <commit>`                 | Creates a commit that is intended to fix a previous commit. When used with `git rebase -i --autosquash`, it will automatically move the fixup commit next to the commit it's fixing and suggest squashing them together.  |


## Working with Remotes

| Command                         | Description                                                                                                                                            |
| ------------------------------- | -----------------------------------------------------------------------------------------------------------------------------------------------------  |
| `git fetch`                     | Fetches all branches and their commits from a remote repository without merging them.                                                                  |
| `git pull`                      | Combines `git fetch` and `git merge`, downloading changes from a remote repository and immediately merging them into your current branch.              |
| `git stash`                     | Temporarily saves changes that are not ready to be committed.                                                                                          |
| `git stash pop`                 | Restores the most recently stashed changes to the working directory.                                                                                   |

## Additional Tools & Tips

1.  **`git diff <file>`:** Shows changes made to a specific file within your working directory.
2.  **`git restore`:**
    -   `git restore <file>`: Restores a deleted file or discards changes in a file.
    -   `git restore -p <file>`: Interactively select hunks to restore or discard in a file.
    -   `git restore .`: Discards all uncommitted changes in the working directory.
3.  **Branch from a Specific Commit:** `git branch <new_branch_name> <commit_id>`
4.  **Checkout with Precision:** Use `git checkout <branch/commit> <file/folder>` to revert files to a specific state or copy them from another branch.
5.  **`git show-branch`:** Displays detailed information about all branches, including their commits and relationships. 
6.  **`git log --follow <file>`:**  Shows the commit history of a file, even if it was renamed or moved.

Let me know if you'd like any further refinements or additions to this cheat sheet! 
