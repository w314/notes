createdAt: "2020-07-12T00:50:28.689Z"
updatedAt: "2021-06-21T19:41:49.662Z"
type: "MARKDOWN_NOTE"
folder: "a2c0786da6dece68d518"
title: "Virtual Machine with Vagrant"
tags: [
  "vagrant"
]
content: '''
  # Virtual Machine with Vagrant
  
  ## Install software
  - To run a virtual machine on windows install [Oracle VM VirtualBox](https://www.virtualbox.org/) to run the virutal machine.
  - Install [Vagrant by HashiCorp](https://www.vagrantup.com/), a command line utility to manage and access virtual machines
  - on 2021/Feb/9 vagrant is compatible with virtual box 6.1.x ([VirtualBox Provider \\| Vagrant by HashiCorp](https://www.vagrantup.com/docs/providers/virtualbox))
  ## Initialize Project Directory
  [Initialize a Project Directory \\| Vagrant - HashiCorp Learn](https://learn.hashicorp.com/tutorials/vagrant/getting-started-project-setup?in=vagrant/getting-started)
  - create directory for vagrant and cd into it
  ```shell
  mkdir vagrantDirectory
  cd vagrantDirectory
  ```
  - create virtual box
  ```shell
  vagrant init hashicorp/bionic64
  ```
  This will create a `Vagrantfile`, meant to be commited to version control
  
  *In case of the following error message:**
  `
  default: Checking for guest additions in VM...
  default: The guest additions on this VM do not match the installed version of
  default: VirtualBox!
  `
  - run 
  ```
  vagrant halt
  ```
  - install 
  ```
  vagrant plugin install vagrant-vbguest
  ```
  `vagrant-vbguest` is a Vagrant plugin which automatically installs the host's VirtualBox Guest Additions on the guest system.
  - reload vagrant
  ```
  vagrant reload
  ```
  
  ## Boot the environment
  [Boot an Environment \\| Vagrant - HashiCorp Learn](https://learn.hashicorp.com/tutorials/vagrant/getting-started-up?in=vagrant/getting-started)
  - bring up virtual machine by:
  ```shell
  vagrant up
  ```
  
  - to check status:
  ```
  vagrant status
  ```
  This will show the virtual machine that is running.
  - to log into virtual machine
  ```
  vagrant ssh
  ```
  - terminate SSH session with `CTRL+d` or `logout`
  #### Removing the virtual machine
  - destroy virtual machine
  ```shell
  vagrant destroy
  ```
  - remove the downloaded box file
  ```shell
  vagrant box list
  vagrant box remove hashicorp/bionic64
  ```
  
  ## The synched folder
  [Synchronize Local and Guest Files \\| Vagrant - HashiCorp Learn](https://learn.hashicorp.com/tutorials/vagrant/getting-started-synced-folders?in=vagrant/getting-started)
  
  When ssh-d into the vagrant, you have your vagrantfile in the shared `\\vagrant` directory.
  You can create a file in your virtual machine:`touch /vagrant/foo`
  Any file created in the shared directory can be accessed from your own machine as well as from the virtual machine when logged in.
  - On your own machine they will be under the project directory you've created in this case: vagrantDirectory.
  - Logged into the virtual machine they are under `/vagrant`
  
  
  
  ## starting vagrant for the first time
  
  - after logging in with `vagrant ssh` you are logged in with standard user vagrant, who has `sudo` capabilities
  - When starting up vagrant for the first time it installs two users in the home directory, `ubuntu` and `vagrant`.
  - every linux machine comes with user name `root`, the administrator user
  - to do administrative tasks we use `sudo` in front of our commands to run them as administrator
  - vagrant sets `port 2222` on our machine to forward to the virtual machine any new user you create can log in with: `ssh <user_name>@127.0.0.1 -p 2222` 
  
  ## first todos
  
  ### update software
  
  - disable the ability to remotely log in as root (usually already done for you)
  1.  update package source list
  ```shell
  sudo apt-get update
  ```
  This will go through all the software installed and check if there are newer versions out there
  2. upgrade software
  ```shell
  sudo apt-get upgrade
  ``` 
  This will go through software under `/etc/apt/sources.list` and checks version of those programs
  3. remove packages no longer required
  ```shell
  sudo apt-get autoremove
  ```
  
  ### install new software
  - use `apt get` to install new software.
  - each linux distribution has its list of its repositories. For ubuntu: [Ubuntu – Package Search Results -- trusty](https://packages.ubuntu.com/search?keywords=trusty)
  
  
  ### add users
  - install `finger` for user management
  ```shell
  sudo apt-get install finger
  ```
  - create user with `sudo adduser <user_name>`
  - check if new user is created with `finger <user_name>`
  - open new terminal window and connect with new user: `ssh <user_name>@127.0.0.1 -p 2222`, afer hitting enter you may be asked an authenticity verification question. Just answer yes.
  - 
  
  
  
  
  
  
  To `package source list` is availabel software for our machine, you can see it by `cat /etc/apt/sources.list`
  
  ### PostgreSQL
  
  - use `psql ` to start 
  - use `ctrl+d` to exit
'''
linesHighlighted: []
isStarred: false
isTrashed: false
