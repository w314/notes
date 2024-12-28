gitlab, ssh

# GitLab


## SSH Connection to GitLab

[GitLab Manual](https://docs.gitlab.com/ee/user/ssh.html)

Check `SSH` version on your local machine
- `ssh -V`
- note capital V in command
- has to be above 6.5 to be a secure version

Generate SSH key pair
- `ssh-keygen -t ed25519 -C "<comment>"`
- comment is optional
- press enter to accept file/directory or choose other
- choose phrase (nickName) for key

