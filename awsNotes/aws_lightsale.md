aws, lightsale, server

# Setup server on `AWS` `Lightsale`

## Setup `Lightsale`
- platform: Linux / Unix
- blueprint: OS only: Ubuntu 20.04 LTS
- change sshkey if you don't like the one offered

### [Setup ssh keys](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-managing-ssh-keys#create-a-custom-key-ssh-keygen)
- generate ssh keys on local machine
- Sign into lightsale
- Go to Account -> Account -> SSH Keys -> Upload Key(under Custome keys)
## Connect to server
- an `ubuntu` username is created 
- [attach static ip to instance](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/lightsail-create-static-ip) to keep the public ip address from changing when the instance is stopped and restarted
- sign in by `ssh ubuntu@<static-ip>

## Configure Linux Server

```bash
# check if any packages need to be updated
sudo apt-get update
# upgrade packages
sudo apt-get upgrade
```
in this case:
- it asked about replacing `.ssh/ssh-cofig and i said replace
- i've upgraded ubuntu

### Second time:
- it asked about replacing `.ssh/ssh-cofig and i said to keep local version
- exit-ed, entered again was told that reboot required




### installing vs code 
```bash
wget 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64' -O /tmp/code_latest_amd64.deb
sudo dpkg -i /tmp/code_latest_amd64.deb
```
<hr>

Error

code depends on libxfixes3; however:
  Package libxfixes3 is not installed

[Solution](https://stackoverflow.com/questions/41877355/visual-studio-code-installation-on-ubuntu-16-04)

```bash
sudo apt-get install -f
```
<hr>
<strong>Error</strong>

`code --version` runs, but running the command `code` does nothing, no error messages either

Gives this error message, when starting from its own directory:
[15821:0214/135323.154184:ERROR:ozone_platform_x11.cc(247)] Missing X server or $DISPLAY [15821:0214/135323.154371:ERROR:env.cc(226)] The platform failed to initialize. Exiting. Segmentation fault (core dumped)

<strong>Possible solution (untried)</strong>

[set DIPSLAY environmental veriable](https://stackoverflow.com/questions/73725613/electron-missing-x-server-or-display)
<hr>

At the end used vscode on local machine ssh-ing to remote server from there.

<strong>Error</strong>

VSCode keeps dropping ssh connection

[Solution](https://earlruby.org/2021/06/fixing-vscode-when-it-keeps-dropping-ssh-connections/)

### Setting up store app

- git was already installed on lightsale
- `git clone https://github.com/w314/storeApp.git store`
- npm was not installed
- `sudo apt install npm`

