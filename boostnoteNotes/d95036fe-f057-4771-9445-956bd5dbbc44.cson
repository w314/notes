createdAt: "2021-02-10T19:26:18.665Z"
updatedAt: "2021-03-02T13:32:11.879Z"
type: "MARKDOWN_NOTE"
folder: "a2c0786da6dece68d518"
title: "Linux"
tags: [
  "linux"
  "security"
  "$PATH"
]
content: '''
  # Linux
  
  ## File System
  - `pwd` show your home directory
  - the `\\` is the root level of the file system
  - you can find `/home` in each linux sytem it houses all the home directories of the users
  -  any file that names starts with a `.` is a hidden file. You can list hidden files with `ls -a`, with details with `ls -al`
  ```
  drwxr-xr-x 4 vagrant vagrant 4096 Feb 10 13:37 .
  drwxr-xr-x 4 root    root    4096 Feb 10 13:37 ..
  -rw-r--r-- 1 vagrant vagrant  220 Apr  9  2014 .bash_logout
  -rw-r--r-- 1 vagrant vagrant 3637 Apr  9  2014 .bashrc
  drwx------ 2 vagrant vagrant 4096 Feb 10 13:37 .cache
  -rw-r--r-- 1 vagrant vagrant  675 Apr  9  2014 .profile
  drwx------ 2 vagrant vagrant 4096 Feb 10 13:37 .ssh
  ```
  - if the first character in the line is `d`, it's a direcory, if it's `-` it's a file
  
  #### $PATH variable
  [EnvironmentVariables - Community Help Wiki](https://help.ubuntu.com/community/EnvironmentVariables)
  `$Path` variable has the list of directories the system will look through to find a command.
  
  ### Main directories
  - `etc` for configuration files
  - `var` for variable files, files that you expect to grow, change in size over time like system and application logs
  - `bin` where executable binaries are stored that are accessible by all users. These are applications you run, like the LS command
  - `sbin` similar to *bin* but these binaries are to only be used by the root user for system administration and maintenance purposes
  - `lib` is for libraries that support the binaries that are located around the system
  - `usr` is for user programs, difference from *bin*, that binaries in *bin* are required for boot-up and system maintenance purposes, those in *usr* are not 
  
  
  
  
  
  ## Security
  - disable remote login access for `root` user
  - create and use user created for you with `sudo` to run administrative tasks. Root is a username everybody knows exists, you use a one that is not known.
  - keep software up to date with new releases
      - most linux distributions do not auto-update the software installed on the system, do it yourslef and test your apps that recent updates don't break you your applications
  
  
  ## Help
  Use `man` before command to know more about that command.
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
