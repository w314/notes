linux, ubuntu, apt,


# Setup New Linux System



## Connect remotely to system
[How to Fix “Connection Refused By Port 22” on Ubuntu 22.04 LTS](https://itsubuntu.com/how-to-fix-connection-refused-by-port-22-on-ubuntu-22-04-lts/)

Port 22 is used by SSH on Ubuntu for communicating with other machines in the network to transfer data. Port 22 is also used to access the remote system.

The most common reason behind this error is  OpenSSH has not being installed on Ubuntu where you are trying to connect.  To see whether OpenSSH is installed or not, run the following command on a remote machine.
```bash
sudo apt list --installed | grep openssh-server
```
If you see nothing printed out on the console, then you do not have it installed. You can easily install OpenSSH using the following command:
```bash
sudo apt install openssh-server -y
```
```bash
sudo systemctl status ssh
```
Now, you can make it active with the following command
```bash
sudo systemctl start ssh
```



## Setup Terminal Profile to change font size
Terminal > Add profile > change font > set new profile default

## Install Google Chrome
Use wget to download the latest Google Chrome .deb package :
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

Install Chrome .deb package on your system:
```bash
sudo apt install ./google-chrome-stable_current_amd64.deb
```

## Instal VSCode with `apt` package manager
1. Update system repository
```bash
sudo apt update
```
Updates the system's repository and ensures, that the latest version of vscode is going to be installed.

2. Install pacakge dependencies
For proper operation, vscode requires you to install package dependencies. Run the following command to resolve package dependencies:
```bash
sudo apt install software-properties-common apt-transport-https wget -y
```

3. Add repository
Run the following command to add the Visual Studio Code repository to your system:
```bash
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```

4. Install vscode
```bash
sudo apt install code
```
  ### Issues with Visual Studio Code on Linux  
  Run `code --verbose` to see error log when it won't start.


## Other Software
1. Git
```bash
sudo apt install git
``` 
Did not install the latest version

2. Python was already installed

3. [npm](https://www.npmjs.com/)
```bash
sudo apt install npm
```

4. [docker](https://docs.docker.com/engine/install/ubuntu/)
5. 

## How to install `tar` files
> `tar` are compressed files
1.  Download file
2.  `untar` it
    - go to `Downloads`
    - `tar -xvf <filename>`
3. it will create a directory for the files, cd into it
    - it can give further instructions in a README 
    - it can be ready to use

