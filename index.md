---
layout: lesson
root: .
title: Unix Shell I - file system basics
minutes: 15
---

## Learning Objectives

- Know what the 'shell' is and how to use the shell to navigate the file system and execute commands
- Understand principles and strategies for working at the command line. 
- Understand how the shell makes computing more reproducible and more powerful

## Lesson - What is the Shell?

The *shell* is a program that presents a command line interface which allows you to control your computer using commands entered with a keyboard instead of controlling graphical user interfaces (GUIs) with a mouse/keyboard combination.

There are many reasons to learn about the shell.

* For most bioinformatics tools, you have to use the shell. There is no graphical interface. If you want to work in genomics you're going to need to use the shell.
* The shell gives you *power*. The command line gives you the power to do your work more efficiently and more quickly.  When you need to do things tens to hundreds of times, knowing how to use the shell is transformative.
* To use remote computers or cloud computing, you need to use the shell.


![Automation](./img/gvng.jpg)

Unix is user-friendly, it's just very selective about who its friends are.


Today we're going to go through how to access Unix/Linux and some of the basic shell commands.

## Starting with the shell

We will spend most of our time learning about the basics of the shell by manipulating some experimental data.

Now we're going to download the data for the tutorial. For this you'll need internet access, because you're going to get it off the web.  

We're going to be working with data on our remote server. After logging on, we'll check out the example data.

Let's go into the sample data  directory

```bash
$ cd dc_sample data
```

'cd' stands for 'change directory'

Let's see what is in here. Type

```bash
$ ls
```

You will see
```bash
    sra_metadata  untrimmed_fastq
```

ls stands for 'list' and it lists the contents of a directory.

There are two items listed.  What are they? We can use a command line argument with `ls` to get more information.

```bash
$ ls -F
sra_metadata/  untrimmed_fastq/
```

Anything with a "/" after it is a directory. Things with a "*" after them are programs.  If there are no decorations, it's a file.

You can also use the command

```bash
$ ls -l
drwxr-x--- 2 dcuser sudo 4096 Jul 30 11:37 sra_metadata
drwxr-xr-x 2 dcuser sudo 4096 Jul 30 11:38 untrimmed_fastq
```

to see whether items in a directory are files or directories. `ls -l` gives a lot more
information too.

Let's go into the untrimmed_fastq directory and see what is in there.

```bash
$ cd untrimmed_fastq
$ ls -F
SRR097977.fastq  SRR098026.fastq
```

There are two items in this directory with no trailing slash, so they are files.


## Arguments

Most programs take additional arguments that control their exact behavior. For example, `-F` and `-l` are arguments to `ls`.  The `ls` program, like many programs, take a lot of arguments. Another useful one is '-a', which show everything, including hidden files.  How do we know what the options are to particular commands?

Most commonly used shell programs have a manual. You can access the
manual using the `man` program. Try entering:

```bash
$ man ls
```

This will open the manual page for `ls`. Use the space key to go forward and b to go backwards. When you are done reading, just hit `q` to quit.

Programs that are run from the shell can get extremely complicated. To see an example, open up the manual page for the `find` program. No one can possibly learn all of these arguments, of course. So you will probably find yourself referring back to the manual page frequently.


## The Unix directory file structure (a.k.a. where am I?)

As you've already just seen, you can move around in different directories or folders at the command line. Why would you want to do this, rather than just navigating around the normal way.

When you're working with bioinformatics programs, you're working with your data and it's key to be able to have that data in the right place and make sure the program has access to the data. Many of the problems people run in to with command line bioinformatics programs is not having the data in the place the program expects it to be.


## Moving around the file system

Let's practice moving around a bit.

We're going to work in that `dc_sample_data` directory.

First we did something like go to the folder of our username. Then we opened
'dc_sample_data' then 'data'

Let's draw out how that went.

Now let's draw some of the other files and folders we could have clicked on.

This is called a hierarchical file system structure, like an upside down tree
with root (/) at the base that looks like this.


![Unix](./img/Slide1.jpg)

That (/) at the base is often also called the 'top' level.

When you are working at your computer or log in to a remote computer,
you are on one of the branches of that tree, your home directory (/home/dcuser)

Now let's go do that same navigation at the command line.

Type

```bash
$ cd
```

This puts you in your home directory. This folder here.

Now using `cd` and `ls`, go in to the 'dc_sample_data' directory and list its contents.

Let's also check to see where we are. Sometimes when we're wandering around in the file system, it's easy to lose track of where we are and get lost.

If you want to know what directory you're currently in, type

```bash
$ pwd
```
This stands for 'print working directory'. The directory you're currently working in.

What if we want to move back up and out of the 'data' directory? Can we just type `cd dc_sample_data`? Try it and see what happens.

To go 'back up a level' we need to use `..`

Type

```bash
$ cd ..
```

Now do `ls` and `pwd`. See now that we went back up in to the 'dc_sample_data'
directory. `..` means go back up a level.

* * * *
**Exercise**

Now we're going to try a hunt.  Find a hidden directory in dc_sample_data list its contents and file the text file in there.  What is the name of the file?

Hint: hidden files and folders in unix start with '.', for example .my_hidden_directory
* * * *


## Examining the contents of other directories

By default, the `ls` commands lists the contents of the working directory (i.e. the directory you are in). You can always find the directory you are in using the `pwd` command. However, you can also give `ls` the names of other directories to view. Navigate to the home directory if you are not already there.

Type:

```bash
$ cd
```
Then enter the command:

```bash
$ ls dc_sample_data
```

This will list the contents of the `dc_sample_data` directory without you having to navigate there.

The `cd` command works in a similar way. Try entering:

```bash
$ cd dc_sample_data/untrimmed_fastq
```

and you will jump directly to `untrimmed_fastq` without having to go through the intermediate directory.


****
**Exercise**

List the 'SRR097977.fastq' file from your home directory without changing directories
****

### Shortcut: Tab Completion

Navigate to the home directory. Typing out directory names can waste a lot of time. When you start typing out the name of a directory, then hit the tab key, the shell will try to fill in the rest of the directory name. For example, type `cd` to get back to your home directly, then enter:

```bash
$ cd dc_<tab>
```

The shell will fill in the rest of the directory name for `dc_sample_data`. Now go to dc_sample_data/untrimmed_fastq

```bash
$ ls SR<tab><tab>
```

When you hit the first tab, nothing happens. The reason is that there are multiple directories in the home directory which start with `SR`. Thus, the shell does not know which one to fill in. When you hit tab again, the shell will list the possible choices.

Tab completion can also fill in the names of programs. For example, enter `e<tab><tab>`. You will see the name of every program that starts with an `e`. One of those is `echo`. If you enter `ec<tab>` you will see that tab completion works.



## Full vs. Relative Paths

The `cd` command takes an argument which is the directory name. Directories can be specified using either a *relative* path or a full *path*. The directories on the computer are arranged into a hierarchy. The full path tells you where a directory is in that hierarchy. Navigate to the home directory. Now, enter the `pwd` command and you should see:

```bash
$ pwd
/home/dcuser
```

which is the full name of your home directory. This tells you that you are in a directory called `dcuser`, which sits inside a directory called `home` which sits inside the very top directory in the hierarchy. The very top of the hierarchy is a directory called `/` which is usually referred to as the *root directory*. So, to summarize: `dcuser` is a directory in `home` which is a directory in `/`.

Now enter the following command:

```bash
$ cd /home/dcuser/dc_sample_data/.hidden
```

This jumps to `.hidden`. Now go back to the home directory (cd). We saw
earlier that the command:

```bash
$ cd dc_sample_data/.hidden
```

had the same effect - it took us to the `hidden` directory. But, instead of specifying the full path (`/home/dcuser/dc_sample_data/data`), we specified a *relative path*. In other words, we specified the path relative to our current directory. A full path always starts with a `/`. A relative path does not.

A relative path is like getting directions from someone on the street. They tell you to "go right at the Stop sign, and then turn left on Main Street". That works great if you're standing there together, but not so well if you're trying to tell someone how to get there from another country. A full path is like GPS coordinates. It tells you exactly where something is no matter where you are right now.

You can usually use either a full path or a relative path depending on what is most convenient. If we are in the home directory, it is more convenient to just enter the relative path since it involves less typing.

Over time, it will become easier for you to keep a mental note of the structure of the directories that you are using and how to quickly navigate amongst them.

***
**Exercise**
Now, list the contents of the /bin directory. Do you see anything familiar in there? 
How can you tell these are programs rather than plain files?
***

## Saving time with shortcuts, wild cards, and tab completion

### Shortcuts

There are some shortcuts which you should know about. Dealing with the
home directory is very common. So, in the shell the tilde character,
"~", is a shortcut for your home directory. Navigate to the `dc_sample_data`
directory:

```bash
$ cd
$ cd dc_sample_data
```

Then enter the command:

```bash
$ ls ~
```

This prints the contents of your home directory, without you having to type the full path. The shortcut `..` always refers to the directory above your current directory. Thus:

```bash
$ ls ..
```

prints the contents of the `/home/dcuser/dc_sample_data`. You can chain these together, so:

```bash
$ ls ../../
```

prints the contents of `/home/dcuser` which is your home directory. Finally, the special directory `.` always refers to your current directory. So, `ls`, `ls .`, and `ls ././././.` all do the same thing, they print the contents of the current directory. This may seem like a useless shortcut right now, but we'll see when it is needed in a little while.

To summarize, while you are in the `shell` directory, the commands `ls ~`, `ls ~/.`, `ls ../../`, and `ls /home/dcuser` all do exactly the same thing. These shortcuts are not necessary, they are provided for your convenience.

### Our data set: FASTQ files

We did an experiment and want to look at sequencing results. We want to be able to look at these files and do some things with them.


### Wild cards

Navigate to the `~/dc_sample_data/data/untrimmed_fastq` directory. This
directory contains our FASTQ files.

The `*` character is a shortcut for "everything". Thus, if you enter `ls *`, you will see all of the contents of a given directory. Now try this command:

```bash
$ ls *fastq
```

This lists every file that ends with a `fastq`. This command:

```bash
$ ls /usr/bin/*.sh
```

Lists every file in `/usr/bin` that ends in the characters `.sh`.

```bash
$ ls *977.fastq
```

lists only the file that ends with '977.fastq'

So how does this actually work? Well...when the shell (bash) sees a word that contains the `*` character, it automatically looks for filenames that match the given pattern. 

We can use the command 'echo' to see wilcards are they are intepreted by the shell.

```bash
$ echo *.fastq
SRR097977.fastq SRR098026.fastq
```

The '*' is expanded to include any file that ends with '.fastq'


### Resources:

Shell cheat sheets:<br>
* [http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/](http://fosswire.com/post/2007/08/unixlinux-command-cheat-sheet/)
* [https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md](https://github.com/swcarpentry/boot-camps/blob/master/shell/shell_cheatsheet.md)

* Explain shell - a web site where you can see what the different components of a shell command are doing.[http://explainshell.com](http://explainshell.com)
* Learn more about cloud computing in bioinformatics [http://www.commandlinefu.com](http://www.commandlinefu.com)


