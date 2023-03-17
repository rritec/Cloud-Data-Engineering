# Hadoop(BigData)(Linux)
1. **[Linux Distributions](#Linux-Distributions)**<br>
2. **[Directory](#Directory)**<br>
3. **[Home work](#Home-work)**<br>
4. 


# Linux Distributions

1. Versions/types/kinds/flavors of Linux operating system are called Linux Flavors/Distributions (also called Linux Distro).
  1. Ubuntu
  2. Debian
  3. Red hat
  4. Fedora
  5. Open SUSE
  6. Cent os

# Directory

1. A directory in Linux is similar to a folder in windows OS
2. A directory’s solo job is to store the files and the related information. 
3. All the files, whether ordinary, special, or sub-directory, are contained in directories.

##### mkdir

1. The mkdir stands for `make directory.`
2. With the help of mkdir command, you can create a new directory wherever you want in your system.
3. Syntax: 
``` bash 

mkdir <dirname>

```
4. Example:
``` bash

mkdir test

```
5. If you will not provide a path then by default your file will be created in your current directory only. 
6. If you want to create your directory some where else, then provide the path of your destination directory will be created there.

7. `Making multiple directories`: You can also create multiple directories simultaneously.
8. Syntax
``` sh

mkdir <dirname1> <dirname2> <dirname3> ..

```
9. create multiple directories `d1 d2 d3`

``` sh

mkdir d1 d2 d3

```
##### mkdir -p

1. Sometimes when you want to create a directory, its parent directory or directories might not exist.
2. With the help of mkdir -p command you can create sub-directories of a directory. 
3. It will create parent directory first, if it doesn't exist. 
4. But if it already exists, then it will not print an error message and will move further to create sub-directories.
5. With mkdir command you have to create every file one by one. 
6. But mkdir -p command will create it at once.
``` sh

mkdir -p ~/country/state/district

```
##### rmdir
1. rmdir stands for ‘remove directory'
2. This command is used to delete a directory. 
3. But will not be able to delete a directory including a sub-directory. 
4. It means, a directory has to be empty to be deleted.
5. syntax
``` sh

	rmdir <dirname>  

```
6.example
``` sh

rmdir testDir

```
##### Removing non-empty dir
1. syntax
``` sh

rm –Rf <dirname>

```
2. example
``` sh 

rm –Rf <country>

```
##### Removing multiple directories
1. You can also remove multiple directories simultaneously.
2. syntax
``` sh

rmdir <dirname1> <dirname2> <dirname3> ..
```
3. example
``` sh 

rmdir d1 d2 d3

```
##### pwd
1. Pwd stands for “print working directory”
2. Linux pwd command displays your location currently you are working on. 
3. You log on to the home directory when you boot your PC
4. It will give the whole path starting from the root ending to the directory.
5. syntax
``` sh

pwd

```
##### cd
1. cd stands for “change directory”
2. Linux cd command is used to change the current directory i.e.;  the directory in which the user is currently working.
3.  syntax
``` sh

cd <dirname>

```
4.  example
``` sh 

cd NewDir

```
##### Home directory
1. The directory in which you find yourself when you first login is called your home directory.
2. You will be doing much of your work in your home directory and subdirectories that you'll be creating to organize your files.
3. cd (or) cd ~  will bring you to the home directory


##### Child & parent directory
1. . (dot) represents the current working directory
2. .. (dot dot) represents the directory one level above the current working directory, often referred to as the parent directory.
3. ![image](https://user-images.githubusercontent.com/20516321/225894581-9dd25e93-3122-47cb-9f83-0f17d648da88.png)

##### cd options
1. dfd


| Option | b |
| ---- | --- |
| cd ~ (or) cd | Brings you to your home directory. |
| cd - | Brings you to your previous directory of the current directory. |
| cd .. | Brings you to the parent directory of current directory. |
| cd / | It takes you to the entire system's root directory. |
| cd ../..  | It will take you two directories up. |

##### Linux path completion
1. Path completion is a very helpful feature in any operating system. 
2. It is made to speed up your typing speed. 
3. You just have to hit 'Tab' key and your command, option or file name that is arguments will be automatically completed or will give you the options.
4. For example, if you want to type 'cd Desktop' you can type 'cd De' and hit Tab. 
5. Your command will be automatically completed.
6. Path completion is extremely helpful in typing long file names where you don't remember the full file name.
7. Some files contain symbols or spaces which is difficult to keep in mind there you can use it.

##### Man & help
1. Man stands for manual which is a reference book of a Linux operating system. 
2. To get help on any command that you do not understand, you can type
3. syntax
``` sh

man <command>

```
4.  example
``` sh 

man rm

```
5. The terminal would open the manual page for that command.
6. Also help can be used to see the list of available options for a command
7. syntax
``` sh

<command> --help

```
8. example
``` sh 

ls --help

```

##### Vi Editor
1. The default editor that comes with the UNIX operating system is called vi (VIsual editor)
2. The UNIX vi editor is a full screen editor and has two modes of operation:
--Command mode:
3. commands which cause action to be taken on the file, and
--Insert mode:
4. in which entered text is inserted into the file.
5. To open a file to see it’s contents:
	Vi <filename>
6. To open the file in read-only mode:
	vi –R <filename>
7. Editing the file:
:q --> to quit(coming out) the file
:wq --> write and quit(saving & coming out)
:w --> write (saving)
dd --> to remove a line
yy --> to copy a line
p --> to paste a line
x  --> to remove a character
:set nu  to see the line numbers
8. Navigating to a line:
:n --> to go to a line number


































# Home work
1. Complete learning path and share the screeshot in whatsapp group [here](https://learn.microsoft.com/en-us/training/paths/shell/?WT.mc_id=portaledu_inproduct_roles)




