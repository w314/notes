# GIT

## [Authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)

- You can access repositories on GitHub from the command line in two ways, HTTPS and SSH, and both have a different way of authenticating. 
- If you authenticate without GitHub CLI, you must authenticate with a personal access token. When Git prompts you for your password, enter your personal access token (PAT). Alternatively, you can use a credential helper like [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md).

### PAThttps://github.com/w314/Notes.git

#### 1. set up PAT [Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
In your GitHub Account: <br>-> 
 Settings (right top corner) <br>-> Developer Settings (bottom of left panel) <br>-> Personal access tokens (on left panel) <br>-> Generate new token (button in top right corner)  
#### 2. store `PAT`
Use `GCM` (*Git Creadential Manager*) to store the `PAT`. (It may already be intstalled)
- [Install Git Creadential 
Manager](https://github.com/GitCredentialManager/git-credential-manager#linux-install-instructions)
    - [download `.deb` package](https://github.com/GitCredentialManager/git-credential-manager/releases/tag/v2.0.785)
    - run
    ```bash
    sudo dpkg -i <path-to-package>
    ```
    ```bash
    git-credential-manager-core configure
    ```
    ```bash
    export GCM_CREDENTIAL_STORE="cache"
    ```

When using `git push` for the first time, a pop-up window comes up, and there is a possiblity to enter the token. After that the token is already stored.
