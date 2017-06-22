---
title: "The Filesystem"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- Navigate the Unix file system.
- Copy and move files.
- Use the history command to review recent commands in the shell.
- Use the nano text editor to modify text files.
- Use arguments to modify the behavior of command line commands.
keypoints:
- "First key point."
---


## The Unix directory file structure (a.k.a. where am I?)

As you've already just seen, you can move around in different directories
or folders at the command line. Why would you want to do this, rather
than just navigating around by clicking on folders as you might usually do.

When you're working with bioinformatics programs, you're working with
your data and it's key to be able to have that data in the right place
and make sure the program has access to the data. Many of the problems
people run in to with command line bioinformatics programs is not having the
data in the place the program expects it to be.


## Moving around the file system

Let's practice moving around a bit.

We're going to work in that `dc_sample_data` directory.

First we did something like go to the folder of our username. Then we opened
'dc_sample_data' then 'data'

Let's draw out how that went.

Now let's draw some of the other files and folders we could have clicked on.

This is called a hierarchical file system structure, like an upside down tree
with root (/) at the base that looks like this.


![Unix](../img/Slide1.jpg)

That (/) at the base is often also called the 'top' level.

When you are working at your computer or log in to a remote computer,
you are on one of the branches of that tree, your home directory (/home/dcuser)

Now let's go do that same navigation at the command line.

Type

     cd

This puts you in your home directory. This folder here.

Now using `cd` and `ls`, go in to the 'dc_sample_data' directory and list its contents.

Let's also check to see where we are. Sometimes when we're wandering around
in the file system, it's easy to lose track of where we are and get lost.

If you want to know what directory you're currently in, type

     pwd

This stands for 'print working directory'. The directory you're currently working in.

What if we want to move back up and out of the 'data' directory? Can we just
type `cd dc_sample_data`? Try it and see what happens.

To go 'back up a level' we need to use `..`

Type

     cd ..

Now do `ls` and `pwd`. See now that we went back up in to the 'dc_sample_data'
directory. `..` means go back up a level.

* * * *
**Exercise**

Now we're going to try a hunt.  Find the hidden directory in dc_sample_data, list its contents, and identify the name of the text file in that directory.

Hint: hidden files and folders in unix start with '.', for example .my_hidden_directory
* * * *


## Examining the contents of other directories

By default, the `ls` commands lists the contents of the working
directory (i.e. the directory you are in). You can always find the
directory you are in using the `pwd` command. However, you can also
give `ls` the names of other directories to view. Navigate to the
home directory if you are not already there.

Type:

    cd

Then enter the command:

    ls dc_sample_data

This will list the contents of the `dc_sample_data` directory without
your having to navigate there.

The `cd` command works in a similar way. Try entering:

    cd
    cd dc_sample_data/untrimmed_fastq

and you will jump directly to `untrimmed_fastq` without having to go through
the intermediate directory.

****
**Exercise**

List the contents of the directory containing the 'SRR097977.fastq' file. Do this from your home directory without leaving that directory.
****

## Full vs. Relative Paths

The `cd` command takes an argument which is the directory
name. Directories can be specified using either a *relative* path or a
full *path*. The directories on the computer are arranged into a
hierarchy. The full path tells you where a directory is in that
hierarchy. Navigate to the home directory. Now, enter the `pwd`
command and you should see:

    /home/dcuser

which is the full name of your home directory. This tells you that you
are in a directory called `dcuser`, which sits inside a directory called
`home` which sits inside the very top directory in the hierarchy. The
very top of the hierarchy is a directory called `/` which is usually
referred to as the *root directory*. So, to summarize: `dcuser` is a
directory in `home` which is a directory in `/`.

Now enter the following command:

    cd /home/dcuser/dc_sample_data/.hidden

This jumps to `.hidden`. Now go back to the home directory (cd). We saw
earlier that the command:

    cd dc_sample_data/.hidden

had the same effect - it took us to the `hidden` directory. But,
instead of specifying the full path
(`/home/dcuser/dc_sample_data/data`), we specified a *relative path*. In
other words, we specified the path relative to our current
directory. A full path always starts with a `/`. A relative path does
not.

A relative path is like getting directions
from someone on the street. They tell you to "go right at the Stop sign, and
then turn left on Main Street". That works great if you're standing there
together, but not so well if you're trying to tell someone how to get there
from another country. A full path is like GPS coordinates.
It tells you exactly where something
is no matter where you are right now.

You can usually use either a full path or a relative path
depending on what is most convenient. If we are in the home directory,
it is more convenient to just enter the relative path since it
involves less typing.

Over time, it will become easier for you to keep a mental note of the
structure of the directories that you are using and how to quickly
navigate amongst them.

***
## Relative Path Resolution

Using the filesystem diagram below, if `pwd` displays `/Users/thing`,
what will `ls ../backup` display?

1.  `../backup: No such file or directory`
2.  `2012-12-01 2013-01-08 2013-01-27`
3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
4.  `original pnas_final pnas_sub`

![File System for Challenge Questions](../fig/filesystem-challenge.svg)

> ## Solution
> 1. No: there *is* a directory `backup` in `/Users`.
> 2. No: this is the content of `Users/thing/backup`,
>    but with `..` we asked for one level further up.
> 3. No: see previous explanation.
>    Also, we did not specify `-F` to display `/` at the end of the directory names.
> 4. Yes: `../backup` refers to `/Users/backup`.
{: .solution}
{: .challenge}
***

***
**Exercise**

Now, list the contents of the /bin directory. Do you see anything
familiar in there?
How can you tell these are programs rather than plain files?

***

## Saving time with shortcuts, wild cards, and tab completion

### Shortcuts

There are some shortcuts which you should know about. Dealing with the
home directory is very common. So, in the shell the tilde character,
""~"", is a shortcut for your home directory. Navigate to the `dc_sample_data`
directory:

    cd
    cd dc_sample_data

Then enter the command:

    ls ~

This prints the contents of your home directory, without you having to
type the full path. The shortcut `..` always refers to the directory
above your current directory. Thus:

    ls ..

prints the contents of the `/home/dcuser/dc_sample_data`. You can chain
these together, so:

    ls ../../

prints the contents of `/home/dcuser` which is your home
directory. Finally, the special directory `.` always refers to your
current directory. So, `ls`, `ls .`, and `ls ././././.` all do the
same thing, they print the contents of the current directory. This may
seem like a useless shortcut right now, but we'll see when it is
needed in a little while.

To summarize, while you are in the `shell` directory, the commands
`ls ~`, `ls ~/.`, `ls ../../`, and `ls /home/dcuser` all do exactly the
same thing. These shortcuts are not necessary, they are provided for
your convenience.
