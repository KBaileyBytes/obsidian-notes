---
tags:
  - note
---
# `= this.file.name` 
---

| Abbreviation   | Name                     | Purpose                                                               | Example                                                      |
| -------------- | ------------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------ |
| `git init`     | Initialize Repository    | Creates a new Git repository                                          | `git init`                                                   |
| `git clone`    | Clone Repository         | Clones a repository into a new directory                              | `git clone <repository-url>`                                 |
| `git status`   | Check Status             | Shows the status of the working directory                             | `git status`                                                 |
| `git add`      | Stage Changes            | Adds changes in the working directory to the staging area             | `git add <file>`                                             |
| `git commit`   | Commit Changes           | Records changes to the repository                                     | `git commit -m "Commit message"`                             |
| `git log`      | View Commit History      | Displays commit logs                                                  | `git log`                                                    |
| `git push`     | Push Changes to Remote   | Uploads local repository content to a remote repository               | `git push <remote-name> <branch-name>`                       |
| `git pull`     | Update Local Repository  | Fetches from and integrates with another repository or a local branch | `git pull <remote-name> <branch-name>`                       |
| `git branch`   | Create Branch            | Creates a new branch                                                  | `git branch <branch-name>`                                   |
| `git checkout` | Switch Branch            | Switches to a specified branch                                        | `git checkout <branch-name>`                                 |
| `git merge`    | Merge Branches           | Combines changes from different branches                              | `git merge <branch-name>`                                    |
| `git rm`       | Remove Files             | Removes files from the working directory and staging area             | `git rm <file>`                                              |
| `git mv`       | Rename Files             | Moves or renames files or directories                                 | `git mv <old-name> <new-name>`                               |
| `git restore`  | Discard Changes          | Discards changes in the working directory                             | `git restore <file>` or `git restore --source=HEAD~1 <file>` |
| `git remote`   | View Remote Repositories | Lists all remote's that are configured.                               |                                                              |

## Common Terms

1. **Repository (Repo)**: A folder that contains your project files along with the revision history of each file. It's where your project's source code resides.
    
2. **Commit**: A snapshot of changes made to files in a repository at a particular point in time. Each commit has a unique identifier (SHA-1 hash) and is accompanied by a commit message describing the changes.
    
3. **Branch**: A separate line of development within a repository. Branches allow you to work on new features, bug fixes, or experiments without affecting the main codebase until changes are ready to be merged.
    
4. **Merge**: The process of integrating changes from one branch into another. It combines the changes made in different branches to create a single unified history.
    
5. **Pull Request (PR)**: A request to merge changes from one branch (usually a feature branch) into another (often the main branch) in a repository. Pull requests facilitate code review and collaboration among team members.
    
6. **Fork**: A copy of a repository in which you can make changes without affecting the original repository. Forking is often used to propose changes to someone else's project via pull requests.
    
7. **Clone**: The process of creating a local copy of a remote repository on your computer. Cloning allows you to work on the repository's code locally.
    
8. **Push**: The process of sending your committed changes from your local repository to a remote repository. Pushing updates the remote repository with your local changes.
    
9. **Pull**: The process of fetching and integrating changes from a remote repository into your local repository. Pulling updates your local repository with changes made by others.
    
10. **Remote**: A version of a repository that is hosted on a server, separate from your local repository. Remotes allow you to collaborate with others by sharing your changes and syncing with their changes.
    
11. **Merge Conflict**: A situation that occurs when Git is unable to automatically merge changes from different branches. Merge conflicts require manual resolution by the user.
    
12. **Checkout**: The process of switching between different branches or reverting files to a specific commit. Checkout allows you to navigate through different states of your project.
    
13. **Staging Area (Index)**: A temporary storage area where changes are prepared before being committed to the repository. Files in the staging area are ready to be included in the next commit.
    
14. **.gitignore**: A file that specifies intentionally untracked files that Git should ignore. Gitignore files are used to exclude files such as compiled binaries and temporary files from being tracked by Git.
    
15. **GitHub**: A web-based platform for hosting and collaborating on Git repositories. GitHub provides features such as pull requests, issue tracking, and project management tools to facilitate collaboration among developers.






---
Created: March 19, 2024
Last Modified: `= this.file.mtime`
