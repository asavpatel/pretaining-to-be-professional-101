
# What Is "The Shell"?

Simply put, the shell is a program that takes commands from the keyboard and gives them to the operating system to perform. In the old days, it was the only user interface available on a Unix-like system such as Linux. Nowadays, we have  _graphical user interfaces (GUIs)_  in addition to  _command line interfaces (CLIs)_  such as the shell.

On most Linux systems a program called  bash (which stands for Bourne Again SHell, an enhanced version of the original Unix shell program,  sh, written by Steve Bourne) acts as the shell program. Besides  bash, there are other shell programs that can be installed in a Linux system. These include:  ksh,  tcsh  and  zsh.

## What's A "Terminal?"

It's a program called a  _terminal emulator_. This is a program that opens a window and lets you interact with the shell. There are a bunch of different terminal emulators you can use. Most Linux distributions supply several, such as:  gnome-terminal,  konsole,  xterm,  rxvt,  kvt,  nxterm, and  eterm.

## Starting A Terminal

Your window manager probably has a way to launch a terminal from the menu. Look through the list of programs to see if anything looks like a terminal emulator. If you are a KDE user, the terminal program is called "konsole," in Gnome it's called "gnome-terminal." You can start up as many of these as you want and play with them. While there are a number of different terminal emulators, they all do the same thing. They give you access to a shell session. You will probably develop a preference for one, based on the different bells and whistles each one provides.

## Testing The Keyboard

OK, let's try some typing. Bring up a terminal window. You should see a  _shell prompt_  that contains your user name and the name of the machine followed by a dollar sign. Something like this:
```{r, engine='bash', count_lines}
[me@linuxbox me]$
```


Excellent! Now type some nonsense characters and press the enter key.
```{r, engine='bash', count_lines}
[me@linuxbox me]$  kdkjflajfks
```
If all went well, you should have gotten an error message complaining that it cannot understand you:

```{r, engine='bash', count_lines}
[me@linuxbox me]$  kdkjflajfks
bash: kdkjflajfks: command not found
```

Wonderful! Now press the up-arrow key. Watch how our previous command "kdkjflajfks" returns. Yes, we have  _command history_. Press the down-arrow and we get the blank line again.

Recall the "kdkjflajfks" command using the up-arrow key if needed. Now, try the left and right-arrow keys. You can position the text cursor anywhere in the command line. This allows you to easily correct mistakes.


## :skull: You're not logged in as root, are you? :skull:

If the last character of your shell prompt is **#** rather than **$**, you are operating as the  _superuser_. This means that you have administrative privileges. This can be potentially dangerous, since you are able to delete or overwrite any file on the system. Unless you absolutely need administrative privileges, do not operate as the superuser.

## Using The Mouse :mouse2:

Even though the shell is a command line interface, the mouse is still handy.

Besides using the mouse to scroll the contents of the terminal window, you can copy text with the mouse. Drag your mouse over some text (for example, "kdkjflajfks" right here on the browser window) while holding down the left button. The text should highlight. Release the left button and move your mouse pointer to the terminal window and press the middle mouse button (alternately, you can press both the left and right buttons at the same time if you are working on a touch pad). The text you highlighted in the browser window should be copied into the command line.

# Navigation

## pwd

Since a command line interface cannot provide graphic pictures of the file system structure, it must have a different way of representing it. Think of the file system tree as a maze, and you are standing in it. At any given moment, you are located in a single directory. Inside that directory, you can see its files and the pathway to its  _parent directory_  and the pathways to the subdirectories of the directory in which you are standing.

The directory you are standing in is called the  _working directory_. To find the name of the working directory, use the  pwd  command.
```{r, engine='bash', count_lines}
[me@linuxbox me]$  pwd  
/home/me
```
When you first log on to a Linux system, the working directory is set to your  _home directory_. This is where you put your files. On most systems, your home directory will be called /home/your_user_name, but it can be anything according to the whims of the system administrator.

To list the files in the working directory, use the  ls  command.
```{r, engine='bash', count_lines}
[me@linuxbox me]$ ls Desktop     Xrootenv.0    linuxcmd
GNUstep     bin           nedit.rpm
GUILG00.GZ  hitni123.jpg  nsmail 
```
I will come back to  ls  in the next lesson. There are a lot of fun things you can do with it, but I have to talk about pathnames and directories a bit first.

## cd

To change your working directory (where you are standing in the maze) you use the  cd  command. To do this, type  cd  followed by the  _pathname_  of the desired working directory. A pathname is the route you take along the branches of the tree to get to the directory you want. Pathnames can be specified in one of two different ways;  _absolute pathnames_  or  _relative pathnames_. Let's look with absolute pathnames first.

An absolute pathname begins with the root directory and follows the tree branch by branch until the path to the desired directory or file is completed. For example, there is a directory on your system in which most programs are installed. The pathname of the directory is /usr/bin. This means from the root directory (represented by the leading slash in the pathname) there is a directory called "usr" which contains a directory called "bin".

Let's try this out:
```{r, engine='bash', count_lines}
[me@linuxbox me]$ cd /usr/bin
[me@linuxbox bin]$ pwd
/usr/bin
[me@linuxbox bin]$ ls 
[                     lwp-request
2to3                  lwp-rget
2to3-2.6              lxterm
a2p                   lz
aalib-config          lzcat
aconnect              lzma
acpi_fakekey          lzmadec
acpi_listen           lzmainfo
add-apt-repository    m17n-db
addpart               magnifier
```
and many more... 

Now we can see that we have changed the current working directory to /usr/bin and that it is full of files. Notice how your prompt has changed? As a convenience, it is usually set up to display the name of the working directory.

Where an absolute pathname starts from the root directory and leads to its destination, a relative pathname starts from the working directory. To do this, it uses a couple of special notations to represent relative positions in the file system tree. These special notations are "." (dot) and ".." (dot dot).

The "." notation refers to the working directory itself and the ".." notation refers to the working directory's parent directory. Here is how it works. Let's change the working directory to /usr/bin again:
```
[me@linuxbox me]$  cd /usr/bin  
[me@linuxbox bin]$  pwd  
/usr/bin
```
O.K., now let's say that we wanted to change the working directory to the parent of /usr/bin which is /usr. We could do that two different ways. First, with an absolute pathname:
```
[me@linuxbox bin]$  cd /usr  
[me@linuxbox usr]$  pwd  
/usr
```
Or, with a relative pathname:
```
[me@linuxbox bin]$  cd ..  
[me@linuxbox usr]$  pwd  
/usr
```
Two different methods with identical results. Which one should you use? The one that requires the least typing!

Likewise, we can change the working directory from /usr to /usr/bin in two different ways. First using an absolute pathname:
```
[me@linuxbox usr]$  cd /usr/bin  
[me@linuxbox bin]$  pwd  
/usr/bin
```
Or, with a relative pathname:
```
[me@linuxbox usr]$  cd ./bin  
[me@linuxbox bin]$  pwd  
/usr/bin
```
Now, there is something important that I must point out here. In almost all cases, you can omit the "./". It is implied. Typing:

[me@linuxbox usr]$  cd bin

would do the same thing. In general, if you do not specify a pathname to something, the working directory will be assumed. There is one important exception to this, but we won't get to that for a while.

## A Few Shortcuts

If you type  cd  followed by nothing,  cd  will change the working directory to your home directory.

A related shortcut is to type  **cd ~_user_name_**. In this case,  cd  will change the working directory to the home directory of the specified user.

Typing  ***cd -***  changes the working directory to the previous one.

### Important facts about file names

1.  File names that begin with a period character are hidden. This only means that  ls  will not list them unless you say  ls -a. When your account was created, several hidden files were placed in your home directory to configure things for your account. Later on we will take a closer look at some of these files to see how you can customize your  _environment_. In addition, some applications will place their configuration and settings files in your home directory as hidden files.  
      
    
2.  File names in Linux, like Unix, are case sensitive. The file names "File1" and "file1" refer to different files.  
      
    
3.  Linux has no concept of a "file extension" like legacy operating systems. You may name files any way you like. However, while Linux itself does not care about file extensions, many application programs do.  
      
    
4.  Though Linux supports long file names which may contain embedded spaces and punctuation characters, limit the punctuation characters to period, dash, and underscore.  **Most importantly, do not embed spaces in file names.**  If you want to represent spaces between words in a file name, use underscore characters. You will thank yourself later.


# Looking Around

Now that you know how to move from working directory to working directory, we're going to take a tour of your Linux system and, along the way, learn some things about what makes it tick. But before we begin, I have to teach you some tools that will come in handy during our adventure. These are:

-   [ls](http://linuxcommand.org/lc3_man_pages/ls1.html)  (list files and directories)
-   [less](http://linuxcommand.org/lc3_man_pages/less1.html)  (view text files)
-   [file](http://linuxcommand.org/lc3_man_pages/file1.html)  (classify a file's contents)

## ls

The  ls  command is used to list the contents of a directory. It is probably the most commonly used Linux command. It can be used in a number of different ways. Here are some examples:  
  

Examples of the ls command
| Command | Result  |
|--|--|
| ls | List the files in the working directory |
| ls /bin | List the files in the /bin directory (or any other directory you care to specify) |
| ls -l | List the files in the working directory in long format |
| ls -l /etc /bin | List the files in the /bin directory and the /etc directory in long format |
| ls -la .. | List all files (even ones with names beginning with a period character, which are normally hidden) in the parent of the working directory in long format |


These examples also point out an important concept about commands. Most commands operate like this:

*command -options arguments*

where  _command_  is the name of the command,  _-options_  is one or more adjustments to the command's behavior, and  _arguments_  is one or more "things" upon which the command operates.

In the case of  ls, we see that  ls  is the name of the command, and that it can have one or more options, such as  -a  and  -l, and it can operate on one or more files or directories.

### A Closer Look At Long Format

If you use the  -l  option with  ls, you will get a file listing that contains a wealth of information about the files being listed. Here's an example:  
  

----------

```
-rw-------   	1 asav  workstation       576	Apr 17 2018 	weather.txt
drwxr-xr-x   	6 asav  workstation      1024 	Oct  9  2018	web_page
-rw-rw-r--   	1 asav  workstation   	76480 	Feb 11 20:41 	web_site.tar

----------     	-------	 -------  	   -------  -------------   ------------
	    |             |        |         |         |             |
	    |             |        |         |         |         File Name
	    |             |        |         |         |
	    |             |        |         |         +---  Modification Time
	    |             |        |         |
	    |             |        |         +-------------   Size (in bytes)
	    |             |        |
	    |             |        +-----------------------        Group
	    |             |
	    |             +--------------------------------        Owner
	    |
	    +----------------------------------------------   File Permissions
```
----------

**File Name** :
 The name of the file or directory.

**Modification Time**  : 
The last time the file was modified. If the last modification occurred more than six months in the past, the date and year are displayed. Otherwise, the time of day is shown.

**Size** :
The size of the file in bytes.

**Group** : 
The name of the group that has file permissions in addition to the file's owner.

**Owner** : 
The name of the user who owns the file.

**File Permissions** : 
A representation of the file's access permissions. The first character is the type of file. A "-" indicates a regular (ordinary) file. A "d" indicates a directory. The second set of three characters represent the read, write, and execution rights of the file's owner. The next three represent the rights of the file's group, and the final three represent the rights granted to everybody else. I'll discuss this in more detail in a later lesson.

## less

less  is a program that lets you view text files. This is very handy since many of the files used to control and configure Linux are human readable. also less doesn't open whole file in memory so it's quick and easy way to check very large files.

### Controlling less

Once started,  less  will display the text file one page at a time. You may use the Page Up and Page Down keys to move through the text file. To exit  less, type "q". Here are some commands that  less  will accept:  
  

Keyboard commands for the less program

| Command | Result |
|--|--|
| Page Up or b | Scroll back one page |
| Page Down or space | Scroll forward one page |
| G | Go to the end of the text file |
| 1G | Go to the beginning of the text file |
| /_characters_ | Search forward in the text file for an occurrence of the specified  _characters_ |
| n | Repeat the previous search |
| h | Display a complete list less commands and options|
| q | Quit

## file

As you wander around your Linux system, it is helpful to determine what kind of data a file contains before you try to view it. This is where the  file  command comes in.  file  will examine a file and tell you what kind of file it is.

To use the  file  program, just type:

file _name_of_file_ 

The  file  program can recognize most types of files, such as:  
  

Various kinds of files

| File Type | Description | Viewable as text? | 
|--|--|--|
| ASCII text | The name says it all | yes |
| Bourne-Again shell script text |  A  bash  script | yes |
| ELF 32-bit LSB core file | A core dump file (a program will create this when it crashes) | no |
| ELF 32-bit LSB executable | An executable binary program | no |
| ELF 32-bit LSB shared object | A shared library | no |
| GNU tar archive | A tape archive file. A common way of storing groups of files. | no, use  tar tvf  to  view listing. |
| gzip compressed data | An archive compressed with  gzip | no |
| HTML document text | A web page | yes |
| JPEG image data | A compressed JPEG image | no |
| PostScript document text | A PostScript file | yes |
| RPM | A Red Hat Package Manager archive | no, use  rpm -q  to examine contents. |
| Zip archive data | An archive compressed with  zip | no |

While it may seem that most files cannot be viewed as text, you will be surprised how many can. This is especially true of the important configuration files. You will also notice during our adventure that many features of the operating system are controlled by shell scripts. In Linux, there are no secrets!

# Manipulating Files

This section will introduce you to the following commands:

-   [cp](http://linuxcommand.org/lc3_man_pages/cp1.html)  - copy files and directories
-   [mv](http://linuxcommand.org/lc3_man_pages/mv1.html)  - move or rename files and directories
-   [rm](http://linuxcommand.org/lc3_man_pages/rm1.html)  - remove files and directories
-   [mkdir](http://linuxcommand.org/lc3_man_pages/mkdir1.html)  - create directories

These four commands are among the most frequently used Linux commands. They are the basic commands for manipulating both files and directories.

Now, to be frank, some of the tasks performed by these commands are more easily done with a graphical file manager. With a file manager, you can drag and drop a file from one directory to another, cut and paste files, delete files, etc. So why use these old command line programs?

The answer is power and flexibility. While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs. For example, how would you copy all the HTML files from one directory to another, but only copy files that did not exist in the destination directory or were newer than the versions in the destination directory? Pretty hard with with a file manager. Pretty easy with the command line:

[me@linuxbox me]$  cp -u *.html destination

## Wildcards

Before I begin with our commands, I want to talk about a shell feature that makes these commands so powerful. Since the shell uses filenames so much, it provides special characters to help you rapidly specify groups of filenames. These special characters are called  _wildcards_. Wildcards allow you to select filenames based on patterns of characters. The table below lists the wildcards and what they select:  

Summary of wildcards and their meanings

| Wildcard | Meaning |
|---|---------------------------------------------------------------------------------|
| * | Matches any characters |
| **?** | Matches any single character | 
| **[_characters_]** | Matches any character that is a member of the set  _characters_. The set of characters may also be expressed as a _POSIX character class_  such as one of the following: <br><br>POSIX Character Classes<br>**[:alnum:]**  Alphanumeric characters<br>**[:alpha:]** Alphabetic characters<br>**[:digit:]** Numerals<br>**[:upper:]** Uppercase alphabetic characters<br>**[:lower:]** Lowercase alphabetic characters  |
| **[!_characters_]** | Matches any character that is not a member of the set  _characters_ |

Using wildcards, it is possible to construct very sophisticated selection criteria for filenames. Here are some examples of patterns and what they match:  
  

Examples of wildcard matching

| **Pattern** | **Matches** |
|--|--|
| * | All filenames |
| g* | All filenames that begin with the character "g" |
| b*.txt | All filenames that begin with the character "b" and end with the characters ".txt" |
| Data??? | Any filename that begins with the characters "Data" followed by exactly 3 more characters |
| [abc]* | Any filename that begins with "a" or "b" or "c" followed by any other characters |
| [[:upper:]]* | Any filename that begins with an uppercase letter. This is an example of a character class. |
| BACKUP.[[:digit:]][[:digit:]] | Another example of character classes. This pattern matches any filename that begins with the characters "BACKUP." followed by exactly two numerals. |
| *[![:lower:]] | Any filename that does not end with a lowercase letter. | 

You can use wildcards with any command that accepts filename arguments.

## cp

The  cp  program copies files and directories. In its simplest form, it copies a single file:

```
[me@linuxbox me]$  cp  _file1 file2_
```
It can also be used to copy multiple files (and/or directories) to a different directory:
```
[me@linuxbox me]$  cp  _file... directory_
```
**A note on notation:**  ... signifies that an item can be repeated one or more times.

Other useful examples of  cp  and its options include:  
  
| **Command** | **Results** |
| -- | -- |
| cp _file1 file2_ | Copies the contents of  _file1_  into  _file2_. If  _file2_  does not exist, it is created;  **otherwise,  _file2_  is silently overwritten with the contents of  _file1_.** |
| cp -i _file1 file2_ | Like above however, since the "-i" (interactive) option is specified, if  _file2_  exists, the user is prompted before it is overwritten with the contents of  _file1_. |
| cp _file1 dir1_ | Copy the contents of  _file1_  (into a file named  _file1_) inside of directory   _dir1_. |
| cp -R _dir1 dir2_ | Copy the contents of the directory  _dir1_. If directory  _dir2_  does not exist, it is created. Otherwise, it creates a directory named  _dir1_  within directory  _dir2_. |

## mv

The  mv  command moves or renames files and directories depending on how it is used. It will either move one or more files to a different directory, or it will rename a file or directory. To rename a file, it is used like this:
```
[me@linuxbox me]$  mv  _filename1 filename2_
```
To move files (and/or directories) to a different directory:
```
[me@linuxbox me]$  mv  _file... directory_
```
Examples of  mv  and its options include:  
  
| **Command** | **Results** |
| -- | -- |
| mv _file1 file2_ | If  _file2_  does not exist, then  _file1_  is renamed  _file2_.  **If  _file2_  exists, its contents are silently replaced with the contents of  _file1_.** |
| mv -i _file1 file2_ | Like above however, since the "-i" (interactive) option is specified, if  _file2_  exists, the user is prompted before it is overwritten with the contents of  _file1_. |
| mv _file1 file2 file3 dir1_ | The files  _file1, file2, file3_  are moved to directory  _dir1_. If  _dir1_  does not exist,  mv  will exit with an error. |
| mv _dir1 dir2_ | If  _dir2_  does not exist, then  _dir1_  is renamed  _dir2_. If  _dir2_  exists, the directory  _dir1_  is moved within directory  _dir2_. |

## rm

The  rm  command removes (deletes) files and directories.
```
[me@linuxbox me]$  rm  _file..._
```
It can also be used to delete directories:
```
[me@linuxbox me]$  rm -r  _directory..._
```
Examples of  rm  and its options include:  
|  **Command** | **Results** | 
| -- | -- |
| rm _file1 file2_ | Delete  _file1_  and  _file2_. |
| rm -i _file1 file2_ | Like above however, since the "-i" (interactive) option is specified, the user is prompted before each file is deleted. |
| rm -r _dir1 dir2_ |  Directories  _dir1_  and  _dir2_  are deleted along with all of their contents. |

  

## :skull: Be careful with rm! :skull:

Linux does not have an undelete command`. Once you delete something with  rm, it's gone. You can inflict terrific damage on your system with  rm  if you are not careful, particularly with wildcards.

**_Before you use  rm  with wildcards, try this helpful trick:_**  construct your command using  _**"ls"**_  instead. By doing this, you can see the effect of your wildcards before you delete files. After you have tested your command with  ls, recall the command with the up-arrow key and then substitute  rm  for  ls  in the command.

## mkdir

The  mkdir  command is used to create directories. To use it, you simply type:
```
[me@linuxbox me]$  mkdir  _directory..._
```


