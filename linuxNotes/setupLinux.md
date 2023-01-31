linux, ubuntu, apt, install, vscode


# Setup New Linux System

## How to Install Linux on Windows machine

Create bootable USB drive using `UNetbootIN`

## How to install `tar` files
> `tar` are compressed files
1.  Download file
2.  `untar` it
    - go to `Downloads`
    - `tar -xvf <filename>`
3. it will create a directory for the files, cd into it
    - it can give further instructions in a README 
    - it can be ready to use




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

## Instal VSCode
### A) BEST SOLUTION
- with `wget` and `dpkg`
- grab and instal latest VSCode:
```bash
wget 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64' -O /tmp/code_latest_amd64.deb
sudo dpkg -i /tmp/code_latest_amd64.deb
```
- can be saved to a file like `auto-update-vscode.sh` and run every time VSCode needs updating
- gets latest version unlike `apt` package manager
### B) with `apt` package manager
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

5. yarn
```bash
npm install --global yarn
```


