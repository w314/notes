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
- sign in by `ssh ubuntu@<public-ip-address>

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

