---
layout: page
title: "The Shell"
comments: true
date: 2014-07-30
---

# The Shell

# Learning Objectives
* Navigate the Unix file system.
* Copy and move files.
* Use the history command to review recent commands in the shell.
* Use the nano text editor to modify text files.
* Use arguments to modify the behavior of command line commands.


## What is the shell?

The *shell* is a program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.

There are many reasons to learn about the shell.

* For most bioinformatics tools, you have to use the shell. There is no
graphical interface. If you want to work in metagenomics or genomics you're
going to need to use the shell.
* The shell gives you *power*. The command line gives you the power to do your work more efficiently and
more quickly.  When you need to do things tens to hundreds of times,
knowing how to use the shell is transformative.
* To use remote computers or cloud computing, you need to use the shell.


![Automation](../img/gvng.jpg)

  Unix is user-friendly. It's just very selective about who its friends are.


Today we're going to go through how to access Unix/Linux and some of the basic
shell commands.

## Information on the shell

shell cheat sheets:<br>
* [http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/](http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/)
* [https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md](https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md)

Explain shell - a web site where you can see what the different components of
a shell command are doing.  
* [http://explainshell.com](http://explainshell.com)
* [http://www.commandlinefu.com](http://www.commandlinefu.com)


## How to access the shell

The shell is already available on Mac and Linux. For Windows, you'll
have to download a separate program.


Mac
---  
On Mac the shell is available through Terminal  
Applications -> Utilities -> Terminal  
Go ahead and drag the Terminal application to your Dock for easy access.

Windows
-------
For Windows, we're going to be using gitbash.  
Download and install [gitbash](http://msysgit.github.io);
Open up the program.

Linux  
-----
The shell is available by default when you connect to your AWS instance.  You should be set.



## Starting with the shell

We will spend most of our time learning about the basics of the shell
by manipulating some experimental data.

Now we're going to download the data for the tutorial. For this you'll need
internet access, because you're going to get it off the web.  

We're going to be working with data on our remote server.


After logging on, let's check out the example data.

Let's go into the sample data directory

      cd dc_sample data

`cd` stands for 'change directory'

Let's see what is in here. Type

      ls

You will see

    sra_metadata  untrimmed_fastq

`ls` stands for 'list' and it lists the contents of a directory.

There are two items listed.  What are they? We can use a command line argument with 'ls' to get more information.

      ls -F
      sra_metadata/  untrimmed_fastq/

Anything with a "/" after it is a directory.  
Things with a "*" after them are programs.  
If there are no decorations, it's a file.

You can also use the command

    ls -l
    drwxr-x--- 2 dcuser sudo 4096 Jul 30 11:37 sra_metadata
    drwxr-xr-x 2 dcuser sudo 4096 Jul 30 11:38 untrimmed_fastq

to see whether items in a directory are files or directories. `ls -l` gives a lot more
information too.

Let's go into the untrimmed_fastq directory and see what is in there.

    cd untrimmed_fastq
    ls -F
    SRR097977.fastq  SRR098026.fastq

There are two items in this directory with no trailing slash, so they are files.


## Arguments

Most programs take additional arguments that control their exact
behavior. For example, `-F` and `-l` are arguments to `ls`.  The `ls`
program, like many programs, take a lot of arguments. Another useful one is '-a',
which show everything, including hidden files.  How do we
know what the options are to particular commands?

Most commonly used shell programs have a manual. You can access the
manual using the `man` program. Try entering:

    man ls

This will open the manual page for `ls`. Use the space key to go
forward and b to go backwards. When you are done reading, just hit `q`
to quit.

Programs that are run from the shell can get extremely complicated. To
see an example, open up the manual page for the `find` program.
No one can possibly learn all of
these arguments, of course. So you will probably find yourself
referring back to the manual page frequently.

### Shortcut: Tab Completion

Typing out file or directory names can waste a
lot of time and it's easy to make typing mistakes. Instead we can use tab complete as a shortcut. When you start typing out the name of a directory, then
hit the tab key, the shell will try to fill in the rest of the
directory name.

For example, type `cd` to get back to your home directly, then enter:

    cd dc_<tab>

The shell will fill in the rest of the directory name for
`dc_sample_data`.

Now change directories to **untrimmed_fastq** in **dc_sample_data**

    cd dc_sample_data
    cd untrimmed_fastq

    ls SR<tab><tab>

When you hit the first tab, nothing happens. The reason is that there
are multiple directories in the home directory which start with
`SR`. Thus, the shell does not know which one to fill in. When you hit
tab again, the shell will list the possible choices.

Tab completion can also fill in the names of programs. For example,
enter `e<tab><tab>`. You will see the name of every program that
starts with an `e`. One of those is `echo`. If you enter `ec<tab>` you
will see that tab completion works.
