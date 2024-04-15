## Source Control Management

> What is source control management? Why is it useful?

`Version control` = Revision control = `Source Control Management` (`SCM`), is a process to manage a collection of source code and its changes.

- manage and keep track of all your source code
- all your changes are being stored in a repository.
- there are 2 types of Version Control Systems
  - **C**entralized **V**ersion **C**ontrol **S**ystem (CVCS)
  - **D**istributed **V**ersion **C**ontrol **S**ystem (DVCS).

The concept of `CVCS` is that it works on a Client-Server relationship. The repository is located in one place and provides access to many clients.

On the contrary, in `DVCS`, every user has a local copy of the repository in addition to the central repo on the server-side.

### Git

- you have the entire history of the project right there on your local disk (DVCS)

#### Git States

> What are the main states that your files can reside in when using Git?

Git has three main `states` that your files can reside in:

- `modified` - you have changed the file but have not committed it to your database yet
- `staged` - you have marked a modified file in its current version to go into your next commit snapshot.
- `committed` - the data is safely stored in your local database

#### Git Project Sections

> What are the main sections of a Git project?

The three main `sections` of a Git project:

- `working tree` (or `working directory`) is a single checkout of one version of the project, downloaded to your local machine.
- `staging area` is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the `“index”`
- `git directory`(a.k.a. `repository folder`)
  - stores the metadata and object database for your project
  - stores the history of all changes made to the files in a Git project
  - name of directory: `.git`
    -the most important part of Git, and it is what is copied when you clone a repository from another computer

#### Git Repository Types

Repository types based on user permissions:

- `Bare` Repositories
  - Software development teams use bare repositories to share changes made by team members.
  - Individual users aren't allowed to modify or create new versions of the repository.

<br>

- `Non-Bare` Repositories
  - With non-bare repositories, users can modify the existing repository and create new versions.
  - By default, the cloning process creates a non-bare repository.<br><br>

#### Git Operations

> What are some common operations you would be performing when using Git?

```shell
# initialize repository
git init

# clone repository
git clone [url] [directory]

# get status of git repository
git status

# stage all files in directory
git add .

# commit changes
git commit -m 'commit message'

# push code to remote repository
git push

# create new branch
git branch new-branch

# move to new branch
git checkout new-branch

# shortcut to create and move to new branch
get checkout -b new-branch

# pull data from remote repository
git pull

# merge branch to master
#  1. move to master first
git checkout master
#  2. merge new branch
git merge new-branch
```

#### Git Bash

- Git Bash is an application for Microsoft Windows environments which provides an emulation layer for a Git command line experience. A package that installs Bash, some common bash utilities, and Git on a Windows operating system.
- `Bash` is an acronym for `Bourne Again Shell`
- `Shell` is a terminal application used to interface with an operating system through written commands.
- `Bash` is a popular default shell on Linux and macOS.
