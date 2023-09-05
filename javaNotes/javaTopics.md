WK7

## common UNIX commands

> What are some common Linux commands? Why are they useful?

```shell
#  list directory content
ls

# change directory
cd

# display current working directory path
pwd

# create directory
mkdir

# create empty file
touch

# echo redirected to file with > will create new file
echo "New file content" > new_file.txt

# view file
cat filename

# create new file
cat > newfile

# copy sourcefile content to destionation file
cat sourcefile > destinationfile

# search string in file
grep mystring myfile

# compare 2 files, output lines that are different
diff file1 file2

# move file1 to directory1
mv file1 directory1
# prompt if we would overwrite a file
mv - i file1 directory1
# do not move if we would overwrite a file
mv -n file1 directory1
# only move if the source file is newer than destination file
mv -u file1 directory1
# create backup of overwritten destination file with same name 1 added to end
mv -b file1 directory1

# rename file1 to file2
mv file1 file2

# copy file1 to file2
cp file1 file2
# flags
# interactive, warn before overwriting
-i
# create backup of destination file
-b
# use force: delete destination file if cannot be opened
-f
# recursive, copy directory with all subdirectories
-r
# preserve characteristics: times of last modification, etc
-p

# delete file
rm file1
# delete directory with all files and subdirectories
rm -r directory1
# force deletion flag
-f



mv
rm

cat
grep
cp
```

## source control management

> What is source control management? Why is it useful?

`Version control` = Revision control = `Source Control Management` (`SCM`), is a process to manage a collection of source code and its changes.

- manage and keep track of all your source code
- all your changes are being stored in a repository.
- there are 2 types of Version Control Systems
  - the Centralized Version Control System (CVCS)
  - Distributed (DVCS).

The concept of `CVCS` is that it works on a Client-Server relationship. The repository is located in one place and provides access to many clients.

On the contrary, in `DVCS`, every user has a local copy of the repository in addition to the central repo on the server-side.

## Git

- you have the entire history of the project right there on your local disk

> What are the main states that your files can reside in when using Git?

Git has three main `states` that your files can reside in:

- `modified` - you have changed the file but have not committed it to your database yet
- `staged` - you have marked a modified file in its current version to go into your next commit snapshot.
- `committed` - the data is safely stored in your local database

> What are the main sections of a Git project?

The three main `sections` of a Git project:

- the `working tree` (or `working directory`, as in the diagram below) is a single checkout of one version of the project, downloaded to your local machine. The working tree is the set of all files and folders a developer can add, edit, rename and delete during application development. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
- the `staging area` is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the `“index”`, but the phrase “staging area” works just as well. (See diagram below)
- `Git directory`(a.k.a. `repository folder`) is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer
  - stores the history of all changes made to the files in a Git project
  - name of directory: `.git`

Two types of Git repositories, based on user permissions:

- Bare Repositories
  - Software development teams use bare repositories to share changes made by team members.
  - Individual users aren't allowed to modify or create new versions of the repository.
- Non-Bare Repositories

  - With non-bare repositories, users can modify the existing repository and create new versions.
  - By default, the cloning process creates a non-bare repository.

  > What are some common operations you would be performing when using Git?

- Understand how to push to repo
- Understand how to use branches
- Understand how to merge

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

### Git Bash

- Git Bash is an application for Microsoft Windows environments which provides an emulation layer for a Git command line experience. A package that installs Bash, some common bash utilities, and Git on a Windows operating system.
- `Bash` is an acronym for `Bourne Again Shell`
- `shell` is a terminal application used to interface with an operating system through written commands.
- `Bash` is a popular default shell on Linux and macOS.

## Algorithm

_Note: The types of algorithms mentioned in the lesson are supplementary to know._

## The common Big O Notations

Factory Pattern
Singleton Pattern
Day 4
_NOTE: You will not be assessed over the algorithm implementation details. Understand them at a high level._
Bubble Sort
Merge Sort
Binary Search
Linear Search
