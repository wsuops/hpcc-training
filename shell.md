---
layout: default
title: The Shell
---

Now that you have logged into the cluster, you are now in what is called ***the shell***.  This shell is a text driven program that will help you navigate the complexities of the operating system.  You type in commands and the shell responds to you with output.

There are many different ***shells*** available for Linux.  By default you will be using the ***bourne-again shell*** shell or ***bash*** which was created as a free replacement to an older shell - ***sh*** - written by a programmer named Bourne.  You can find many great tutorials online that will teach you how to navigate in ***bash***.

* [Unix tutorial for beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/index.html)
* [Bash guide for beginners](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/)
* [Advanced bash scripting guide](http://www.tldp.org/LDP/abs/html/)
 
Since there are many tutorials on how to use bash out there already, we will only cover a few common commands that you will use in file management.  When you first log into the system, you will be greeted by a banner and a prompt as well as some additional information about how much storage you have available (we will cover that later).

```text
$ ssh go.cougs@hpclogin1
go.cougs@hpclogin1's password: 
Last login: Mon Jul 28 12:10:06 2014 from 134.121.10.42
          __      __ ___  _   _   _  _  __    ___  ___
          \ \    / // __|| | | | | || || _ \ / __|/ __|
           \ \/\/ / \__ \| |_| | | __ ||  _/| (__| (__
            \_/\_/  |___/ \___/  |_||_||_|   \___|\___|
            
 *****************************************************************
 * Access to electronic resources at Washington State University *
 * is restricted to faculty, staff and students, or individuals  *
 * authorized by the University or its affiliates. Use of this   *
 * system is subject to all policies and procedures set forth by *
 * Wasington State  University. These policies are located at:   *
 *                                                               *
 * http://infotech.wsu.edu/about/policies/computeruse.html       *
 *                                                               *
 * Unauthorized use is prohibited and may result in              *
 * administrative or legal action.  Washington State University  *
 * may monitor the use of this system for purposes related to    *
 * security management, system operations, and intellectual      *
 * property compliance.                                          *
 *****************************************************************
 
 QUESTIONS? Please submit all questions, requests, and system 
            issues to: hpc.support@wsu.edu.

 VOL          TOTAL     AVAIL   TOTAL %    YOUR     YOUR   YOUR %
              SPACE     SPACE     USAGE   USAGE    QUOTA    QUOTA
 HOME       74500.0   34308.0    53.95%   112.0   5120.0    2.19%
 SCRATCH    33467.0    7234.0    78.38%     0.0      0.0     0.0%
 
$
```

***Note:  When creating this tutorial, my prompt was "$", the commands you will be typing are found to the right of the "$".  Don't type the prompt.***

### Viewing the command help pages

At anytime you can view the help pages for the commands that will be used throughout the tutorial to get information about what the command does, options, and even some examples by typing ***man*** (manual) and then the command name.  In otherwords, to find out more information on the ***ls*** command that we will be using next, type:

```text
$ man ls
```

Use the up and down arrows on your keyboard to go forward and backward and use the ***Q*** key to exit the manual

### List the files or folders in your directory

At this point you should have no visible files or folders in your home directory.  You can use the ***ls*** or 'list' command to check:

```text
$ ls
```

As you can see there was nothing returned, but there are some files there.  Linux and Unix have the concept of *hidden files* that do not show up in the regular output.  You can see your hidden files by adding an option to the ***ls*** command that will tell ***ls*** to also show hidden files.

```text
$ ls -a
.              .bash_logout   .clcbio     .lesshst  .rvm       .viminfo      .zlogin
..             .bash_profile  .curlrc     .profile  .ssh       .Xauthority   .zshrc
.bash_history  .bashrc        .install4j  .psrc     .tempstor  .x-formation
```

Most of these files contain configuration data for other programs and you may or may not have all of them.  Notice all of the hidden files start with a *period*.

There are a couple of other files of interest here as well.  Notice the ```.``` and the ```..```?  These represent the current directory and the parent directory.

#### Additional options
There are many options for ls, but some of the options that I have found most useful are the ```-l```, ```-t``` option and the ```-r``` option.  The ```-t``` options tells ```ls``` to sort by decending time and ```-r``` will reverse it.  The ```-l``` option will use a long list format and give you information such as permissions and modification times.  If you have a directory with a large amount of files and you need to see which ones have been accessed recently (and when) just type:

```text
$ ls -altr
```

Your newest files will be listed at the bottom.

### Creating a new folder

Folders are used by Linux to organize files.  To create a new folder, use can use the command ***mkdir*** or 'make directory'.  In Linux Make a folder called 'tutorial' and check to see if it is there.

```text
$ mkdir tutorial
$ ls
tutorial
```

### Enter the folder

You can use the ***cd*** command or 'change directory' to navigate through your folders.  To move into the tutorial folder you just created, type:

```text
$ cd tutorial
```

If you type ***cd*** without a folder name, it will automatically take you back to the top of your home directory.  

You may also want to move back up a directory.  To do this you can use the special file "***..***" (you may have noticed this in the output of ***ls -a*** above).  The two dots represent the *parent* or *containing* folder and can be used like this:

```text
$ cd ..
```
When you type ```ls``` and press enter, you should see the tutorials directory that you created earlier.  Now use ```cd``` to change back to the tutorials directory that you created.

### The smart way to change directories

There are many times that you will run accross cases where you will want to move in and out of several directories.  It can be tough to keep track of the directories that you have entered and left.  The ```pushd``` command can actually keep track of where you have been like breadcrumbs by pushing your current location on to a stack befor it moves to the next directory.  You can then use the ```popd``` to go back to the last location that was pushed.

To test this out make a few more directories:

```text
$ mkdir -p pushtest/{one,two,three,four}/{a,b,c,d}
```

There's a bit of handwaving over this command, but needless to say this is a quick way to recursively create a directory structure that is three levels deep. The numbered directories will each have an a, b, c, and d directory.

Use ```pushd``` to wind your way through the directories and see what happens.  Then use ```popd``` to return to where you were.  When you pop back out all the way you may see:

```text
$ popd
-bash: popd: directory stack empty
```

### Get the tutorial files

Before we go any further, there are files that we will be using for this series of tutorials, you can get them by cloning the training repository.  Some of you may not know what this means, but we will explain what this is doing in a later tutorial.  For now, just copy the command and type it into your terminal just the way it appears here.

```text
$ git clone https://github.com/wsuops/hpcc-training.git
```

Once this is done, you should have a folder named ***hpcc-training*** in your tutorials directory.

```text
$ ls
hpcc-training
```

### Different ways to interact your files

The files that we are going to be using are found in the hpcc-training directory so lets change to it.

```text
cd hpcc-training
```

There are many different ways to access the information stored in your files.  The most common are the ***cat***, ***more***, ***less***, ***head*** and ***tail*** commands.  To view the file contents of hello.txt file that is in the directory run the ```cat``` command with the filename as the argument:

```text
$ cat hello.txt
Hello
```

The command ***cat*** stands for *concatenate* and can take as many files as you want.  You can concatenate the output of many files together by running the cat command with all of the files as arguments:

```text
$ cat hello.txt world.txt 
Hello
World
```

This command does not actually change your files.  It outputs the contents to the screen.  You can capture this output and put it into a new file by using a method called ***redirection***.  To *redirect* the output to a new file you can use ***>*** of ***>>*** after the command with the name of a new file.  The single ***>*** will overwrite all the contents in the file with the new contents you are redirecting into it, while the double will append the new contents to the end of the file. 

```text
$ cat hello.txt world.txt > helloworld.txt
$ cat helloworld.txt 
Hello
World
$ cat hello.txt world.txt >> helloworld.txt
$ cat helloworld.txt 
Hello
World
Hello
World
```

For large files, the ***cat*** command will output all of the file contents without stoping.

```text
$ cat testdata/shakespeare-comedy-7.txt
```

You can use the ***more*** command to page through the contents of a large file.  The ***less*** command is a paging utility like the ***more*** command, but it also allows you to page backwards.  The ***head*** and ***tail*** command show the first and last few lines of a file.  You can control the number of lines shown by adding a dash and then the number of lines (e.g. ***-10***)


You can then use the following commands:

```text
$ more testdata/shakespeare-comedy-7.txt
$ less testdata/shakespeare-comedy-7.txt
$ head -20 testdata/shakespeare-comedy-7.txt
$ tail -20 testdata/shakespeare-comedy-7.txt
```

When using ***more*** or ***less*** you can press the ***Q*** key to exit before the end of the file.

### Copying files

Use the ```cp``` command to copy one of our shakespeare files to the current directory:

```text
$ cp testdata/shakespeare-comedy-7.txt .
```
To copy a directory you can use ***-r*** to copy all files recursively.

### Removing files and directories

Use the ***rm*** command to remove files

```text
$ ls
hello.txt  helloworld.txt  shakespeare-comedy-7.txt  world.txt
$ rm helloworld.txt 
$ ls
hello.txt  shakespeare-comedy-7.txt  world.txt
$
```

To remove a directory you will use the same command but use the ***-r*** option to recursivly remove all of the files in the directory at the same time.  If you do not specify the ***-r*** when trying to remove a directory the command will fail.

```text
$ mkdir -p removeme
$ ls
hello.txt  removeme  shakespeare-comedy-7.txt  world.txt
$ rm removeme
rm: cannot remove `removeme': Is a directory
$ rm -r removeme
$ ls
hello.txt  shakespeare-comedy-7.txt  world.txt
```

### Renaming and moving your files

To rename a file you can use the ***mv*** (move) command or the ***rename*** command.  Move is the simplest form of renaming a file, to test this out type ***mv*** with the original file name and the new file name:

```text
$ ls
hello.txt  moved  shakespeare-comedy-7.txt  world.txt
$ mv world.txt World.txt
$ ls
hello.txt  moved  shakespeare-comedy-7.txt  World.txt

```

The rename command gives you a little more flexibility when it comes to renaming multiple files at the same time.  Let's say that you wanted to take all of your text files in your directory and rename them to have a *.backup* extension before you started creating new ones.  You could use the ***rename*** command to take the .txt extension and turn it into .txt.backup

```text
$ ls
hello.txt  moved  shakespeare-comedy-7.txt  World.txt
$ rename .txt .txt.backup *.txt
$ ls
hello.txt.backup  moved  shakespeare-comedy-7.txt.backup  World.txt.backup
```

*Note the asterisk in \*.txt.  This is called a wildcard and in this context means all files that have the extension 'txt'.  For additional information on wildcards see [this tutorial](http://www.ee.surrey.ac.uk/Teaching/Unix/unix4.html)*

You can also move or rename entire directories along with their contents.

```text
$ mkdir -p moveme/{1,2,3,4}
$ ls moveme
1  2  3  4
$ mv moveme moved
$ ls moved
1  2  3  4
```