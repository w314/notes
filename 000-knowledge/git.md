git

# GIT

## Git Branching
Branching means you diverge from the main line of development and continue to do work without messing with that main line.

### Git Rebase
An alternative to the git merge command.
- only rebase local changes that haven't been pushed/shared with other
- rebasing rewrites the commit history

```bash
# Switch to the branch you want to rebase
git checkout feature-branch

# Rebase your branch onto master
git rebase master
```

This will take all changes that were committed on feature-branch, and replay them on master. If there are any conflicts, Git will pause and allow you to resolve those conflicts before continuing.

Remember, it's a good practice to only rebase local changes that haven't been pushed/shared with others. This is because rebasing rewrites the commit history, which can cause confusion and conflicts if the commits are already in the public repository.
## GIT Questions


- What is branching? Why is it useful?

    - What are the commands related to branching?

- What are merge conflicts? How do they arise?

    - What must we do to resolve merge conflicts?

- What is a pull request?

- What do we define in .gitignore files?