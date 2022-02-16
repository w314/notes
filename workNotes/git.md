# GIT

## PAT

### To set up PAT (Personal Access Token)
[Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

### Store PAT
Use `GCM` (*Git Creadential Manager*) to store the `PAT`.
- [Install Git Creadential Manager](https://github.com/GitCredentialManager/git-credential-manager#linux-install-instructions)

- [Set `GCM_CREDENTIAL_STORE` variable](https://github.com/GitCredentialManager/git-credential-manager/blob/main/docs/credstores.md)
```bash
git config --global credential.credentialStore secretservice
```
When using `git push` a pop-up window asked if I want to authenticate with the browser and when chose that authentication was succesful.

