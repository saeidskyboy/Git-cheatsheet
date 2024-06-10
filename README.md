# Git reference
All commands you need from 0 to pro
Note:  git commands must be run inside the folder that contains all the code. 

## Creating commits
In GIt, version = commit
Version history = commit history

| Command | Description |
| - | - |
| `git init`                                         | Git will start tracking all changes in the current folder |
| `git status`                                       | Show all changes since the previous commit |
| `git add <file/folder>`                            | Pick changes to go into next commit |
| `git add <file>`                                   | Pick individual file |
| `git add <folder/>`                                | Pick all files inside a folder (and subfolders) |
| `git add .`                                        | Pick all files (in folder command line is running in) |
| `git commit  -m "message"`                         | Creates a commit with a message attached |
| `git commit  -m "message" --amend`                 | Update previous commit instead of creating new one |
| `git log`                                          | View the commit history (current and previous versions but next versions, if we role back to a version. i.e. we have 5 versions and we want to role back to version 3 (by `git checkout <commit hash>`, so with `git log` we only will see version 1,2 and 3 |
| `git log  --all`                                   | Show all commits (not just current branch)|
| `git log  --all --graph`                           | Show branching visually in the command line|

   
## Configure Name & Email for commits

| Command | Description |
| - | - |
| `git config --global user.name "skyboy"`                       | Set user name |
| `git config --globall user.email "skyboy@example.com"`         | set user email |

## Staging Area
it contains changes that will go into the next commit

| working => staging | staging => commit history | staging => working |
| - | - | - |
| `git add  .` | `git commit  -m "message"` | `git reset  <file/folder>` |
| | `git reset  file` | |
| | `git reset  folder/` | | |
| | `git reset  .` | |

## Staged Changes
| Command | Description |
| - | - |
| `git add file.txt`                        | Stage file |
| `git add -p`|--patch file.txt`            | Stage some but not all changes in a file |
| `git mv file1.txt file2.txt`              | Move/rename file |
| `git rm --cached file.txt`                | Unstage file |
| `git rm --force file.txt`                 | Unstage and delete file |
| `git reset HEAD`                          | Unstage changes |
| `git reset --hard HEAD`                   | Unstage and delete changes |
| `git clean -f\|--force -d`                | Recursively remove untracked files from the working tree |
| `git clean -f\|--force -d -x`             | Recursively remove untracked and ignored files from the working tree |

## Uploading Code to GitHub 
| Command | Description |
| - | - |
| `git config  --global credential.username  <username>`    | Configure our GitHub username so we can get access to our Github repository |
| `git remote add  <remote_name> <url>` | Link a local repository to a remote repository and give a name for this link. i.e. ![Screen Shot 2024-06-10 at 22 10 55](https://github.com/saeidskyboy/Git-cheatsheet/assets/97639248/65c6f4d9-b523-401d-85f8-a14c90b13c9d) links a local repository to a GitHub repository (located at the url https://github.com/saeidskyboy/DevOps) and gives it a name "update5" |
| `git remote`                              | List all remote repositories that are linked |
| `git remote -v`                           | List all remote repositories with more details |
| `git remote remove  <remote_name>`        | Removes a link to a remote repository |
| `git remote remove  origin`               | Removes the link to the remote repository named "origin" |
| `git push -u <remote_name> <branch>`        | Upload a branch of our git version history to our remote repository. The -u flag (short for --set-upstream) sets up a tracking relationship between your local and remote branches, making future pushes easier.

|
