# GIT

## [Authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)

- You can access repositories on GitHub from the command line in two ways, HTTPS and SSH, and both have a different way of authenticating. 
- If you authenticate without GitHub CLI, you must authenticate with a personal access token. When Git prompts you for your password, enter your personal access token (PAT). Alternatively, you can use a credential helper like [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md).

### PAT

#### 1. set up PAT [Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

#### 2. store `PAT`
Use `GCM` (*Git Creadential Manager*) to store the `PAT`.
- [Install Git Creadential Manager](https://github.com/GitCredentialManager/git-credential-manager#linux-install-instructions)

When using `git push` a pop-up window comes up, and there is a possiblity to enter the token.
