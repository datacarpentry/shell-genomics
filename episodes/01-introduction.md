---
title: "Introducing the Shell"
teaching: 20
exercises: 0
questions:
- "What is a command shell and why would I use one?"
- "How can I move around on my computer?"
- "How can I see what files and directories I have?"
- "How can I specify the location of a file or directory on my computer?"
objectives:
- "Describe key reasons for learning shell."
- "Navigate your file system using the command line."
- "Demonstrate the use of tab completion, and explain its advantages."
keypoints:
- "The shell gives you the ability to work more efficiently by using keyboard commands rather than a GUI."
- "pwd, ls, and cd are useful commands to navigate a file system."
- "Tab completion can reduce errors from mistyping and make work more efficient in the shell."
---

## What is a shell and why should I care?

A *shell* is a computer program that presents a command line interface
which allows you to control your computer using commands entered
with a keyboard instead of controlling graphical user interfaces
(GUIs) with a mouse/keyboard combination.

There are many reasons to learn about the shell.

* Many bioinformatics tools can only be used through a command line interface, or 
have extra capabilities in the command line version that are not available in the GUI.
This is true, for example, of BLAST, which offers many advanced functions only accessible
to users who know how to use a shell.  
* The shell makes your work less boring. In bioinformatics you often need to do
the same set of tasks with a large number of files. Learning the shell will allow you to
automate those repetitive tasks and leave you free to do more exciting things.  
* The shell makes your work less error-prone. When humans do the same thing a hundred different times
(or even ten times), they're likely to make a mistake. Your computer can do the same thing a thousand times
with no mistakes.  
* The shell makes your work more reproducible. When you carry out your work in the command-line 
(rather than a GUI), your computer keeps a record of every step that you've carried out, which you can use 
to re-do your work when you need to. It also gives you a way to communicate unambiguously what you've done, 
so that others can check your work or apply your process to new data.  
* Many bioinformatic tasks require large amounts of computing power and can't reallistically be run on your
own machine. These tasks are best performed using remote computers or cloud computing, which can only be accessed
through a shell.

![Automation](../img/gvng.jpg)

In this lesson you will learn how to use the command line interface to move around in your file system. 

## How to access the shell

On a Mac or Linux machine, you can access a shell through a program called Terminal, which is already available
on your computer. If you're using Windows, you'll need to download a separate program to access the shell.


> ## Accessing the shell
> Mac
> ---  
> On Mac the shell is available through Terminal  
> Applications -> Utilities -> Terminal  
> Go ahead and drag the Terminal application to your Dock for easy access.
> 
> Windows
> -------
> For Windows, we're going to be using gitbash.  
> Download and install [gitbash](http://msysgit.github.io);
> Open up the program.
> 
> Linux  
> -----
> The shell is available by default when you connect to your AWS instance.  You should be set.
{: .callout}


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

## More information on the shell

shell cheat sheets:<br>
* [http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/](http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/)
* [https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md](https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md)

Explain shell - a web site where you can see what the different components of
a shell command are doing.  
* [http://explainshell.com](http://explainshell.com)
* [http://www.commandlinefu.com](http://www.commandlinefu.com)

