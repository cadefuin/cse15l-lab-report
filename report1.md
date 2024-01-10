# Lab Report 1: Remote Access and FileSystem (Week 1)
This lab consisted of exploring the basic filesystem commands `cd`, `ls`, and `cat`.

## `cd` Command
Using `cd` with no arguments:
```
[user@sahara ~]$ cd
[user@sahara ~]$ pwd
/home
```
*When the command was run, the working directory was `/home`. The lack of arguments indicates that the directory should be changed to the default, which in this case was `/home`. The command `cd` itself did not produce an output, but the same prompt `[user@sahara ~]$` was displayed again. This is not an error, as the working directory was not changed.*

Using `cd` with a path to a directory as an argument:
```
[user@sahara ~]$ cd ./lecture1/
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
*When the command was run, the working directory was `/home`. The argument was a path to the folder `lecture1`. The change in directory is reflected by the new prompt `[user@sahara ~/lecture1]$` as it shows the new working directory. This is not an error.*

Using `cd` with a path to a file as an argument:
```
[user@sahara ~/lecture1]$ cd ./messages/en-us.txt
bash: cd: ./messages/en-us.txt: Not a directory
```
*When the command was run, the working directory was `/home/lecture1`. The argument was a path to the file `en-us.txt` which is not a directory and thus cannot be used as a working directory. This is an error.*

## `ls` Command
Using `ls` with no arguments:
```
[user@sahara ~]$ ls
lecture1
```
*When the command was run, the working directory was `/home`. The lack of arguments indicates that the terminal should list items in the working directory. The only item `lecture1` is outputted, which is not an error.*

Using `ls` with a path to a directory as an argument:
```
[user@sahara ~]$ ls ./lecture1/
Hello.class Hello.java messages README
```
*When the command was run, the working directory was `/home`. The argument indicates that the terminal should list items in the directory `./lecture`. The terminal successfully displays all these items, so there is no error.*

Using `ls` with a path to a file as an argument:
```
[user@sahara ~]$ ls /home/lecture1/messages/en-us.txt
/home/lecture1/messages/en-us.txt
```
*When the command was run, the working directory was `/home`. The argument points to a file, which does not contain other files. The output is the path of the given file, which makes sense as it is the only file at the end of the path, so there is no error*

## `cat` Command
Using `cat` with no arguments:
```
[user@sahara ~]$ cat

```
*When the command was run, the working directory was `/home`. With no arguments, there is nothing to concatenate, therefore the blank output makes sense. There is no error.*

Using `cat` with a path to a directory as an argument:
```
[user@sahara ~]$ cat /home/lecture1/
cat: /home/lecture1/: Is a directory
```
*When the command was run, the working directory was `/home`. Since the argument is a path to a directory, which is a collection of other directories and files, there is no specific information to concatenate. Thus there is an error.*

Using `cat` with a path to a file as an argument:
```
[user@sahara ~]$ cat /home/lecture1/messages/en-us.txt
Hello World!
```
*When the command was run, the working directory was `/home`. The file specified by the path does have information that can be concatenated. The file contents are outputted properly, so there is no error.*
