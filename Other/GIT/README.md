# Git
- [git rebase vs git merge](#git_rebase_vs_git_merge)
- [git stash](#git_stash)

## git rebase vs git merge <a name="git_rebase_vs_git_merge"></a>
`git merge` makes an additional commit that merges both branches, `git rebase` takes the changes from the source branch and puts them on top of the target branch. Result in code is usually the same.


## git stash <a name="git_stash"></a>
`git stash` save changes made to a working directory that are not ready to be committed to the repository. It can be particularly useful when you are in the middle of working on a feature or fixing a bug and need to switch to another task or fix an urgent issue. By stashing your changes, you can safely switch to another branch or task, and then come back to your original changes later without losing any work. You can later retrieve the saved changes by using `git stash apply `or `git stash pop` commands. 
