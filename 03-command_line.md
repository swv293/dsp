# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

* show current working directory path : **pwd**
* creating a directory : **mkdir <_dir name_>**
* deleting a directory : **rmdir <_dir name_>**
* creating a file using `touch` command : **touch <_filename_>**
* deleting a file : **rm <_filename_>**
* renaming a file : **mv -f <_source_> <_target_>**
* listing hidden files: __ls -ld .?*__
* copying a file from one directory to another : **cp <_source_> <_target_>**

_My entries to the cheat sheet_

* Help manual on any command: **man <_command_>**
* Find file: **locate <_filename_>**
---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`     : Lists the content of the current directory or specified directory.

`ls -a`  : Lists the files in a directory including the dot files. 

`ls -l`  : Lists the files in long format, including details such as read/write access to individual directories, date last modified and size amongst others.

`ls -lh` : Same as above but with the -h option expresses size in bytes, kilobytes etc. 

`ls -lah`: Same as above but with all the dot files included as well, due to -a option.

`ls -t`  : Same as the ls command, but is sorted in the order of when the files were modified last (lastest first), before arranging in a lexicological manner.

`ls -Glp`: Returns a colorised list in the long format (-l) with directories colored differently than files (-G). In addition the -p option returns the directories with a / in the end. 


---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

* `ls -li`
* ` `
* ` `
* ` `
* ` `


---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

`xargs` is a command line utility which take items from standard input and carries out the specific task assigned to it one at a time. In other words, it helps set up an execution pipeline.

One way to use this function is shown below: 

```
echo 'file1 file2 file3' | xargs mkdir
```


 

