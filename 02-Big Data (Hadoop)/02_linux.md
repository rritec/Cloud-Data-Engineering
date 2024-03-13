# Hadoop(BigData)(Linux)
**[1 Linux Distributions](#1-Linux-Distributions)**<br>
**[2 Directory](#2-Directory)**<br>
**[3 Man and help](#3-Man-and-help)**<br>
**[4 Vi Editor](#4-Vi-Editor)**<br>
**[5 Linux Files](#5-Linux-Files)**<br>
**[6 Home work](#6-Home-work)**<br>


# 1. Linux Distributions

1. Versions/types/kinds/flavors of Linux operating system are called Linux Flavors/Distributions (also called Linux Distro).
  1. Ubuntu
  2. Debian
  3. Red hat
  4. Fedora
  5. Open SUSE
  6. Cent os

# 2 Directory

1. A directory in Linux is similar to a folder in windows OS
2. A directory’s solo job is to store the files and the related information. 
3. All the files, whether ordinary, special, or sub-directory, are contained in directories.

**mkdir**

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
**mkdir -p**

1. Sometimes when you want to create a directory, its parent directory or directories might not exist.
2. With the help of mkdir -p command you can create sub-directories of a directory. 
3. It will create parent directory first, if it doesn't exist. 
4. But if it already exists, then it will not print an error message and will move further to create sub-directories.
5. With mkdir command you have to create every file one by one. 
6. But mkdir -p command will create it at once.
``` sh

mkdir -p country/state/district

```
**rmdir**
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
**Removing non-empty dir**
1. syntax
``` sh

rm –Rf <dirname>

```
2. example
``` sh 

rm –Rf <country>

```
**Removing multiple directories**
1. You can also remove multiple directories simultaneously.
2. syntax
``` sh

rmdir <dirname1> <dirname2> <dirname3> ..
```
3. example
``` sh 

rmdir d1 d2 d3

```
**pwd**
1. Pwd stands for “print working directory”
2. Linux pwd command displays your location currently you are working on. 
3. You log on to the home directory when you boot your PC
4. It will give the whole path starting from the root ending to the directory.
5. syntax
``` sh

pwd

```
**cd**
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
**Home directory**
1. The directory in which you find yourself when you first login is called your home directory.
2. You will be doing much of your work in your home directory and subdirectories that you'll be creating to organize your files.
3. cd (or) cd ~  will bring you to the home directory


**Child & parent directory**
1. . (dot) represents the current working directory
2. .. (dot dot) represents the directory one level above the current working directory, often referred to as the parent directory.
3. ![image](https://user-images.githubusercontent.com/20516321/225894581-9dd25e93-3122-47cb-9f83-0f17d648da88.png)

**cd options**
1. dfd


| Option | b |
| ---- | --- |
| cd ~ (or) cd | Brings you to your home directory. |
| cd .. | Brings you to the parent directory of current directory. |
| cd / | It takes you to the entire system's root directory. |
| cd ../..  | It will take you two directories up. |

**Linux path completion**
1. Path completion is a very helpful feature in any operating system. 
2. It is made to speed up your typing speed. 
3. You just have to hit 'Tab' key and your command, option or file name that is arguments will be automatically completed or will give you the options.
4. For example, if you want to type 'cd Desktop' you can type 'cd De' and hit Tab. 
5. Your command will be automatically completed.
6. Path completion is extremely helpful in typing long file names where you don't remember the full file name.
7. Some files contain symbols or spaces which is difficult to keep in mind there you can use it.

# 3 Man and help
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
5. To close the **manual** type **q** from keyboard
6. The terminal would open the manual page for that command.
7. Also help can be used to see the list of available options for a command
8. syntax
``` sh

<command> --help

```
8. example
``` sh 

ls --help

```

# 4 Vi Editor



1. The default editor that comes with the UNIX operating system is called vi (VIsual editor)
2. The UNIX vi editor is a full screen editor and has two modes of operation:
    1. **Command mode:** commands which cause action to be taken on the file
    2. **Insert mode:** in which entered text is inserted into the file.
5. To open a file to see it’s contents
	``` sh 
	Vi <filename>
	
	```
6. To open the file in read-only mode
	``` sh
	vi –R <filename>
	```
7. Editing the file:
``` sh
 :q --> to quit(coming out) the file
:wq --> write and quit(saving & coming out)
:w --> write (saving)
dd --> to remove a line
yy --> to copy a line
p --> to paste a line
x  --> to remove a character
:set nu  to see the line numbers

```
8. Navigating to a line:
	`:n --> ` to go to a line number

# 5 Linux Files
**Linux Files-Topics**
1. Creating empty files 
2. Creating file contents
3. Removing files
4. Copying files
5. Moving files
6. Renaming files

**Touch-Creating single empty file**
1. touch command is a way to create empty files .
2. syntax
``` sh

<touch <filename>  

```
3. example
``` sh 

touch myfile1 

```

**Touch-Creating multiple empty files**
1. To create multiple files just type all the file names with a single touch command followed by enter key.
2.  syntax
``` sh

touch <filename1> <filename2>

```
3. example
``` sh 

touch myfile1 myfile2

```
**Cat-Creating file contents**
1. Cat command is used to create file contents
2. To create a new file, use the command
    -cat > filename
    -Add content
    -Press 'ctrl + d' to return to command prompt.

**Cat-Displaying files content**
1. Cat command is used to display files contents of a file
2.  syntax
``` sh

cat <filename1>

```
3. example
``` sh 

cat myfile1

```
4. Cat command is used to display files contents of a file that’s present in any directory path
5. example
``` sh 

cat /home/Admin/Month/ThisMonth.txt

```
**rm**
1. Removing file
2. Removing multiple files
3. Removing files with same extension
4. Removing non-empty dir

**Rm-removing file**
1. The 'rm' means remove. 
2. This command is used to remove a file. 
3. The command line doesn't have a recycle bin or trash unlike other GUI's to recover the files.
4. Hence, be very much careful while using this command. 
5. Once you have deleted a file, it is removed permanently.
6. syntax
``` sh

rm <filename>  

```
3. example
``` sh 

rm myfile1 

```

**Rm-removing multiple files**
1. rm can be used as follows to remove multiple files at a time
2. syntax
``` sh

rm <filename1> <filename2> 

```
3. example
``` sh 

rm myfile1 myfile2

```
**Rm-removing files with same extension**
1. rm can be used to remove all the files ending with same extensions like .pdf, .txt,.log, etc.
2.  syntax
``` sh

rm *<extension>

```
3. example
``` sh 

rm *.txt 

```

**Rm-Removing non-empty dir**
1. With rm '-r' option, you can delete a directory having sub directories inside it. 
2. So you don't need to delete sub-directories manually.
3. Non-empty directories can be removed recursively as follows: 
4. syntax
``` sh

rm –R <dirname>
(or)
rm –r <dirname>

```
5. example
``` sh 

rm –R country
(or)
rm –r country

```
**Rm-Removing file/dir forcefully**
1. If a file has read-only access, then while removing it will  ask for permission whether to delete or not. 
2. However, the file will be deleted after getting permission (Y)
3. But by giving command rm -rf it will delete that particular file having read-only access without asking for permission.
4. rm -rf command deletes directory forcefully. 
5. It means a file or directory will be deleted anyhow even if it has read-only permission.
6. To delete a file forcefully, use command:
7. syntax
``` sh

rm -f <file name>

```
8. To delete a directory forcefully, use command:
9. syntax
``` sh

rm -rf <directory name> 

```

**cp**
1. Copying file
2. Copying file into a directory
3. Copying multiple files into a directory
4. Copying multiple files with same extension into a directory
5. Copying dir along with sub-dirs
6. Copying multiple files with similar file names into a directory

**cp-copying file**
1. 'cp' means copy. 
2. 'cp cp-copying file' command is used to copy a file or a directory.
3. To copy a file into the same directory syntax will be:
4. syntax
``` sh

cp <existing file name> <new file name>

```
5. example
``` sh 

cp oldfile.txt newfile.txt

```

**cp-copying file into a directory**
1. cp can be used to copy a file into a directory 
2. To copy a file into a directory the syntax will be:
3. syntax
``` sh

cp <filename>  <dirpath>

```
4. example
``` sh 

cp month.txt /home/Admin/Month

```

**cp-copying multiple files into a directory**
1. cp can be used to copy multiple files into a directory 
2. To copy a multiple files into a directory the syntax will be:
3. syntax
``` sh

cp <filename1> <filename2>  <dirpath>

```
4. example
``` sh 

cp month.txt week.txt /home/Admin/August

```

**cp-copying multiple files with same extension into a directory**
1. cp can be used to copy multiple files with same extension into a directory 
2. To copy a multiple files with same extension into a directory the syntax will be:
3. syntax
``` sh

cp *.txt  <dirpath>

```
4. example
``` sh 

cp *.txt /home/Admin/August

```

**cp-copying dir along with sub-dirs**
1.Option 'r' with the copy command can be used to copy a directory including all its content from a source directory to the destination directory.
2. syntax
``` sh

cp -r <sourceDirectory> <destinationDirectory>  
	
cp <sourceDirectory>/* <destinationDirectory>

```
3. example
``` sh 

cp -r JulyTempData       /home/Admin/AugTempData
cp  JulyTempData/*      /home/Admin/AugTempData 

```

**cp-copying multiple files with similar file names into a directory**
1. cp can be used to copy multiple files with similar file names into a directory 
2. To copy a multiple files with similar file names into a directory the syntax will be:
3. example
``` sh 

cp file* /home/Admin/File

```
**mv**
1. Moving a file
2. Moving multiple files
3. Moving multiple files with same extension
4. Moving all files from one dir to other dir
5. Renaming a file & directory

**Mv-moving a file**
1. Linux mv command is used to move existing file or directory from one location to another
2. syntax
``` sh

mv <filename> <dirname>
mv <dirname>/<filename> <dirname>

```
3. example
``` sh 

mv file1 dir1
mv /home/Admin/file2 dir2

```
##### 



















































# 6 Home work
1. Complete learning path and share the screeshot in whatsapp group [here](https://learn.microsoft.com/en-us/training/paths/shell/?WT.mc_id=portaledu_inproduct_roles)




