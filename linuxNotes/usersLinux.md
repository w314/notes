
  # Linux Users
  
  If starting vitual machine with vagrant after logging in with `vagrant ssh` you are logged in with standard user vagrant, who has `sudo` capabilities
  - When starting up vagrant for the first time it installs two users in the home directory, `ubuntu` and `vagrant`.
  - vagrant sets `port 2222` on our machine to forward to the virtual machine any new user you create can log in with: `ssh <user_name>@127.0.0.1 -p 2222` 
  
  ## Users
  - every linux machine comes with user name `root`, the administrator user,  root users directory is under `/root/`
  - standard users home directories are under `/home/<user_directory>`
  - user information is stored under `/etc/passwd` in the following format
  `<username>:x:<user_id>:<group_id>:<user_description>:<user_home_directory>:<user_default_shell>`
  (at second place used to be the encypted password, but nowadays it's replaced with a character in ubunty trusty and 'x')
  - to do administrative tasks we use `sudo` in front of our commands to run them as administrator
  
  ### Create User
  - install `finger` for user management:
  ```shell
  sudo apt-get install finger
  ```
  - add user with `sudo adduser <user_name>`. Check that user is added with `finger student`
  - force user to change its password next time it logs in:
  `sudo passwd -e <user_name>`
  
  
  ### Add `sudo` capabilities:
  - [Sudoers - Community Help Wiki](https://help.ubuntu.com/community/Sudoers)
  - looking at the sudoers file `sudo cat /etc/sudoers`, you'll see instructions
  - in ubuntu if tells you to include new sudo users in the `/etc/sudoers.d` directory, if you do this any ubuntu update that updates won't delete you users if the regular sudoers file is overwritten.
  - if you list  `sudo ls /etc/sudoers.d`, you'll a  `vagrant` virtual machine you'll see a file *vagrant* is already there.
  - copy  this vagrant file and name it student
  `sudo cp /etc/sudoers.d/vagrant /etc/sudoers.d/<user_name>` 
  - edit it with nano to change the user name inside the file, that's what counts, file name itself doesn't count
  `nano /etc/sudoers.d/<user_name>`
  change name, save with ctrl-o
  
  ### Add SSH key to user
  - generate ssh key pair on local machine not server whith: `ssh-keygen`
  - Add file name with path `\\c\\Users\\<user_name>\\.ssh\\<file_name>`
  - add password to file if desired
  - two file will be created, one with the extension *.pub*, that is the public key
  - to add public key manually: log into linux with the user
      - in home directory create *.ssh* directory, where all key related files must be stored
      `mkdir .ssh`
      - create file *autohorized_keys* where all your public keys must be stored, whith one key per line
      `touch .ssh/authorized_keys`
      - copy public key from your local machine
      - add it to *authorized_keys*
      `nano .ssh/authorized_keys`
  - protect your *.ssh* directory and *authorized_keys* files
      - `chmod 700 .ssh`
      - `chmod 644 .ssh/authorized_keys`
  - user can now log in with:
  `ssh <user_name>@127.0.0.1 -p 2222 -i ~/.ssh/<ssh_key_file_name>`
  
  ### Forcing key based authentication
  - the *ssh* is the service running on the server listening to all of the *ssh* connections
  - you have to edit its configuration file:
  `sudo nano /etc/.ssh/sshd_config`
  - find this line and set it to no:
  `PasswordAuthentication no`
  - have to restart the service for the changes to take effect:
  `sudo service ssh restart`
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
