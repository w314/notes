git

# GIT

## [Authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)

- You can access repositories on GitHub from the command line in two ways, HTTPS and SSH, and both have a different way of authenticating. 
- If you authenticate without GitHub CLI, you must authenticate with a personal access token. When Git prompts you for your password, enter your personal access token (PAT). Alternatively, you can use a credential helper like [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md).

### PAT

#### 1. set up PAT [Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

#### 2. store `PAT`
Use `GCM` (*Git Creadential Manager*) to store the `PAT`.
- [Install Git Creadential Manager](https://github.com/GitCredentialManager/git-credential-manager#linux-install-instructions)

When using `git push` for the first time, a pop-up window comes up, and there is a possiblity to enter the token. After that the token is already stored.

  ## Git Tag
  - [Git - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
  - to list tags: `git tag`
  - to add tag to previous commit:
  `git tag -a v1.2 -m 'new version'`
    - `-a` for annonated tag
    - `-m` for message
  
  
  ## Branches
  
  >**Switching branches carries uncommitted changes with you**. 
  
  - either commit first
  - or run `git checkout .` to undo them
  - or run `git stash` before switching. (You can get your changes back with `git stash apply`)
  
  ### Merging Branches
  
  Checkout the branch you want to merge the other branch into (master) and run:
  `git merge <branch-to-be-merged>`
  ## Undos and Ignore
  
  #### Reset unstaged changes
  `git reset --hard`
  deletes all changes made since last commit
  
  #### Drop staged (unstage) changes
  `git restore <file>` like it shows in the `git status` instructions
   
  
  ### File in .gitignore not ignored
  .gitignore only ignores files that are not part of the repository yet. If you already git added some files, their changes will still be tracked. To remove those files from your repository (but not from your file system) use `git rm --cached` on them.
  
  ## Git configuration
  **see git configuration**:
  `git config --list`
  
  **configure git**:
  `git config --global user.name "Piroska Werner"`
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false

