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
| `git add <file>`                                   | Pick individual file |
| `git add <folder/>`                                | Pick all files inside a folder (and subfolders) |
| `git add .`                                        | Pick all files (in folder command line is running in) |
| `git commit  -m "message"`                         | Creates a commit with a message attached |
| `git commit  -m "message" --amend`                 | Update previous commit instead of creating new one |
| `git commit -a -m "message"` we can make it short `gcam "message"`                      | Add and commit only files which were changed |
| `git log`                                          | View the commit history (current and previous versions but next versions, if we role back to a version. i.e. we have 5 versions and we want to role back to version 3 (by `git checkout <commit hash>`, so with `git log` we only will see version 1,2 and 3 |

## Compare
| Command | Description |
| - | - |
| `git diff`                                | See difference between working area and current branch |
| `git diff HEAD HEAD~2`                    | See difference between te current commit and two previous commits |
| `git diff main other`                     | See difference between two branches |

## View
| Command | Description |
| - | - |
| `git log`                                 | See commit list |
| `git log --patch`                         | See commit list and line changes |
| `git log -a --decorate --oneline --graph` | See commit visualization (save it as a "log a dog ;)" |
| `git log --grep skyboy`                   | See commits with "skyboy" in the message |
| `git reflog`                              | it will expose details about our local commit history |
| `git show HEAD`                           | Show the current commit |
| `git show HEAD^` or `git show HEAD~1`     | Show the previous commit |
| `git show HEAD^^` or `git show HEAD~2`    | Show the commit going back two commits |
| `git show main`                           | Show the last commit in a branch |
| `git show 5720fdf`                        | Show named commit |
| `git blame file.txt`                      | See who changed each line and when |


   
## Configure Name & Email for commits

| Command | Description |
| - | - |
| `git config --global user.name "skyboy"`                       | Set user name |
| `git config --globall user.email "skyboy@example.com"`         | set user email |

## Switch between stage/working areas
it contains changes that will go into the next commit

| working => staging | staging => commit history | staging => working | working => remove the  changes |
| - | - | - | - |
| `git add  file` | `git commit -m "message"` | `git reset  file` | `git checkout --  file` |
| `git add  folder/` | |`git reset  folder/` | `git checkout --  folder/` |
| `git add  .` | |`git reset  .` | `git checkout --  .` |

## Staged Changes
| Command | Description |
| - | - |
| `git add file.txt`                        | Stage file |
| `git add -p`|--patch file.txt`            | Stage some but not all changes in a file |
| `git mv file1.txt file2.txt`              | Move/rename file |
| `git rm --cached file.txt`                | Unstage file |
| `git rm --force file.txt`                 | Unstage and delete file |
| `git reset HEAD`                          | Unstage changes, in another word it will reset our env back to the way it was that commit |
| `git reset --hard HEAD`                   | Unstage and delete changes |
| `git revert <commit ID>`                  | it will remove all changes that were happened with that particular commit, and will keep the other changes (before/after that commit) i.e. if there are commit 1, 2, 3, 4 and we will do `git revert <commit ID 2>` we only remove all changes which were took in place via commit 2 without touching rest of commits (1, 2, 4) |
| `git cherry-pick <commit ID>`             | it will bring back the reverted changes (exactly opposite of `git revert`) | 
| `git clean -f\|--force -d`                | Recursively remove untracked files from the working tree |
| `git clean -f\|--force -d -x`             | Recursively remove untracked and ignored files from the working tree |

## Uploading Code to GitHub
Install "[Git Large File Storage](https://git-lfs.com)" extension to handle your large files (files more than 100 Mb), it will replace large files with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise
| Command | Description |
| - | - |
| git config  --global credential.username  <username>      | NOT recommended |
| `git config --global credential.helper store`             | GitHub now recommends using a credential helper to manage authentication. This provides a more secure and streamlined way to store your credentials => https://github.com/settings/tokens => create a token then use it instead of password |
| `git remote add  <remote_name> <url>` | Link a local repository to a remote repository and give a name for this link. i.e. ![Screen Shot 2024-06-10 at 22 10 55](https://github.com/saeidskyboy/Git-cheatsheet/assets/97639248/65c6f4d9-b523-401d-85f8-a14c90b13c9d) links a local repository to a GitHub repository (located at the url https://github.com/saeidskyboy/DevOps) and gives it a name "update5" |
| `git remote`                              | List all remote repositories that are linked |
| `git remote -v`                           | List all remote repositories with more details |
| `git remote remove  <remote_name>`        | Removes a link to a remote repository |
| `git remote remove  origin`               | Removes the link to the remote repository named "origin" |
| `git lfs track .`                         | this will track all files in current directory |
| `git push -u <remote_name> <branch>`      | Upload a branch of our git version history to our remote repository. The -u flag (short for --set-upstream) sets up a tracking relationship between your local and remote branches, making future pushes easier.
| `git push <remote name> <commit name (main/master/HEAD)> --set-upstream` | Sets up a shortcut for this branch and remote repository Next time you are on the  main branch and you run  git push  , it will automatically push the main  branch to  origin ![Screen Shot 2024-06-11 at 15 10 38](https://github.com/saeidskyboy/Git-cheatsheet/assets/97639248/e8a8e426-796b-45c7-bb83-ef62b3ef59a8), with this next time we only need to run `git push` and it memorize "origin mster" and automatically will push it.

## Branches
| Command | Description |
| - | - |
| `git branch skyboy`                            | Create a new branch with name "skyboy"|
| `git branch -d skyboy`                         | Deletes "skyboy" branch |
| `git switch last_sky`                          | Switch to branch "last_sky"|
| `git switch -c lastjump`                       | Create "lastjump" branch and will switch to it |
| `git restore skyboy.js`                        | Undo all changes on the skyboy.js file |
| `git checkout skyboy.js`                       | Undo all changes on the skyboy.js file |
| `git merge Y`                                  | If you will be in branch X and execute `git merge Y` branch Y will merge into X (Y will no capture any data/changes from x) |
| `git rebase origin/brnach2`                    | rewrites the history of your local branch, making it look like your commits were created after the latest remote commits |

## Pros and Cons of Merge vs. Rebase:
| Feature | Merge | Rebase |
| - | - | - |
| History:                             | Preserves the entire history, including the branching structure | Creates a linear history, which can be easier to read but loses the context of when branches were created |
| Conflicts:                           | Resolves conflicts in a single merge commit | Resolves conflicts one commit at a time, which can be more time-consuming but allows for more granular control |
| Collaboration:                       | Generally safer for collaborative work, as it doesn't rewrite history | Can cause issues if you rebase commits that have already been pushed to a shared repository |
