createdAt: "2019-08-07T16:46:32.548Z"
updatedAt: "2021-07-12T19:45:31.778Z"
type: "MARKDOWN_NOTE"
folder: "b682d2d60df3a4241969"
title: "Shell Programming"
tags: [
  "shell"
]
content: '''
  # Shell Programming
  
  ## Working with Directories
  - display current working directory: `pwd`
  - `cd <directory name>` move to directory. Without directory name it'll take you to your home directory.
  - list directories `ls`
    - list hidden files too: `ls -a`
    - list all files in long format `ls-al`
    - list files with details: `ls -ls`
  - **NO UNDO!** remove non-empty directory: `rm -rf`
  -r option removes directories and and their contents recursively
  -f option ignores nonexistent files and arguments, never prompts for anything
  NO UNDO
  - rename directory
  `mv 'old direcory name' 'new directory name'`
  - **Copy Files or Directories**
  `cp -avr 'source' 'destination'`
  -a : save attributes (last modification date etc)
  -v : verbose messages
  -r : copy directories recursively
  If you copy last change date will be the time of copy and the owner will be the one making the copy.
  Using `-p` preserves the original setup.
  To copy a directory use the `-r` flag.
  - Move Files
  To move all files, but not folders:
  If you are interested in moving all files (but not folders) from Downloads folder to Videos folder, use this command
  `find ~/Downloads/ -type f -exec mv -t ~/Videos \\{\\} \\+`
  ## Working with files with 
  
  ### writing to files - `echo`
  - `echo "adding this text to file" > my_file.txt `
  if using the `>` redirection operator the file is created if it doesn't exits. The output from 'echo' is added at the start of the file **overwriting any previous content**.
  - `echo "adding this text to file" >> my_file.txt`
  if we use the `>>` redirection operator, the file is created if it doesn't exiss like before, but the **output is added to the end of the file and no previous content is deleted**.
  - echo-ing special characters:
  Put the whole string in single quotes
  This works for all chars except single quote itself. To escape the single quote, close the quoting before it, insert the single quote, and re-open the quoting.
  `'I'\\''m a s@fe $tring which ends in newline'`
  
  ### delete file / `rm`
  `rm my_file.txt`
  
  
  1. **rename** file:
  `mv 'old file name' 'new file name'`
  1. **edit** file: `vi 'file name'`
  3. **search** in file: `gre`p
  - The grep filter searches a file for a particular pattern of characters, and displays all lines that contain that pattern. The pattern that is searched in the file is referred to as the regular expression (grep stands for globally search for regular expression and print out).
  
  
  - Syntax: `grep [options] pattern [files]`
  Options:
  -c : This prints only a count of the lines that match a pattern
  -h : Display the matched lines, but do not display the filenames.
  -i : Ignores, case for matching
  -l : Displays list of a filenames only.
  -n : Display the matched lines and their line numbers.
  -v : This prints out all the lines that do not matches the pattern
  -e exp : Specifies expression with this option. Can use multiple times.
  -f file : Takes patterns from file, one per line.
  -E : Treats pattern as an extended regular expression (ERE)
  -w : Match whole word
  -o : Print only the matched parts of a matching line,
   with each such part on a separate output line.
  
  
  - Sample Commands
  Consider the below file as an input.
  `$cat > geekfile.txt
  'unix is great os. unix is opensource. unix is free os.
  learn operating system.
  Unix linux which one you choose.
  uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.'`
  1. Case insensitive search : The -i option enables to search for a string case insensitively in the give file. It matches the words like “UNIX”, “Unix”, “unix”.
  
  `$grep -i "UNix" geekfile.txt`
  Output:
  >unix is great os. unix is opensource. unix is free os.
  Unix linux which one you choose.
  uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
  2. Displaying the count of number of matches : We can find the number of lines that matches the given string\\pattern
  
  `$grep -c "unix" geekfile.txt`
  Output:
  
  >2
  3. Display the file names that matches the pattern : We can just display the files that contains the given string\\pattern.
  `$grep -l "unix" *`
  or
  `$grep -l "unix" f1.txt f2.txt f3.xt f4.txt`
  Output:
  >geekfile.txt
  4. Checking for the whole words in a file : By default, grep matches the given string\\pattern even if it found as a substring in a file. The -w option to grep makes it match only the whole words.
  `$ grep -w "unix" geekfile.txt`
  Output:
  >unix is great os. unix is opensource. unix is free os.
  uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
  5.  Displaying only the matched pattern : By default, grep displays the entire line which has the matched string. We can make the grep to display only the matched string by using the -o option.
  `$ grep -o "unix" geekfile.txt`
  Output:
  >unix
  unix
  unix
  unix
  unix
  unix
  
  6. Show line number while displaying the output using grep -n : To show the line number of file with the line matched.
  `$ grep -n "unix" geekfile.txt`
  Output:
  >1:unix is great os. unix is opensource. unix is free os.
  4:uNix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
  
  7. Inverting the pattern match : You can display the lines that are not matched with the specified search sting pattern using the -v option.
  `$ grep -v "unix" geekfile.txt`
  Output:
  >learn operating system.
  Unix linux which one you choose.
  
  8. Matching the lines that start with a string : The ^ regular expression pattern specifies the start of a line. This can be used in grep to match the lines which start with the given string or pattern.
  `$ grep "^unix" geekfile.txt`
  Output:
  >unix is great os. unix is opensource. unix is free os.
  
  9. Matching the lines that end with a string : The $ regular expression pattern specifies the end of a line. This can be used in grep to match the lines which end with the given string or pattern.
  `$ grep "os$" geekfile.txt`
  
  10.Specifies expression with -e option. Can use multiple times :
  `$grep –e "Agarwal" –e "Aggarwal" –e "Agrawal" geekfile.txt`
  
  11. -f file option Takes patterns from file, one per line.
  `$cat pattern.txt
  Agarwal
  Aggarwal
  Agrawal`
  `$grep –f pattern.txt  geekfile.txt`
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
