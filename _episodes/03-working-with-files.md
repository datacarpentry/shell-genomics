---
title: "Working with Files"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- Use the wild card shortcut
- Use the history command to view recently used commands
- View, copy, move, and create files
keypoints:
- "First key point."
---

## Working with Files

### Our data set: FASTQ files

Now that we know how to navigate around our directory structure, lets
start working with our sequencing files. We did a sequencing experiment and 
have two results files, which are stored in our `untrimmed_fastq` directory. 

### Wild cards

Navigate to your `untrimmed_fastq` directory.

~~~
$ cd ~/dc_sample_data/untrimmed_fastq
~~~
{: .bash}

We are interested in looking at the FASTQ files in this directory. We can list
all files with the fastq extension using the command:

~~~
$ ls *.fastq
~~~
{: .bash}

~~~
SRR097977.fastq  SRR098026.fastq
~~~
{: .output}

The `*` character is a wildcard character which stands for "everything". 
Thus, `*.fastq` matches every file that ends with `fastq`. 

This command: 

~~~
$ ls *977.fastq
~~~
{: .bash}

~~~
SRR097977.fastq
~~~
{: .output}

lists only the file that ends with `977.fastq`.

We can use the command `echo` to see how the wildcard character is intepreted by the
shell.

~~~
$ echo *.fastq
~~~
{: .bash}

~~~
SRR097977.fastq SRR098026.fastq
~~~
{: .output}

The `*` is expanded to include any file that ends with `.fastq`.

This command:

~~~
$ ls /usr/bin/*.sh
~~~
{: .bash}

Lists every file in `/usr/bin` that ends in the characters `.sh`.

> ## Exercise
> Do each of the following tasks from your current directory using a single
> `ls` command for each.
> 
> 1.  List all of the files in `/usr/bin` that start with the letter 'c'.
> 2.  List all of the files in `/usr/bin` that contain the letter 'a'. 
> 3.  List all of the files in `/usr/bin` that end with the letter 'o'.
>
> Bonus: List all of the files in 'usr/bin' that contain the letter 'a' or the
> letter 'c'.
> 
> Hint: The bonus question requires a Unix wildcard that we haven't talked about
> yet. Trying searching the internet for information about Unix wildcards to find
> what you need to solve the bonus problem.
> 
> > ## Solution
> > 1. ls /usr/bin/c*
> > 2. ls /usr/bin/*a*
> > 3. ls /usr/bin/*o
> > Bonus: 
> > 
> {: .solution}
{: .challenge}


## Command History

If you want to repeat a command that you've run recently, you can access previous
commands using the up arrow on your keyboard to go back to the most recent
command. Likewise, the down arrow takes your forwards in the command history.

A few more useful shortcuts: 

`^-C` (Control-C) will cancel the command you are writing, and give you a 
fresh prompt.

`^-R` will do a reverse-search through your command history.  This
is very useful.

You can also review your recent commands with the `history` command, by entering:

~~~
$ history
~~~
{: .bash}

to see a numbered list of recent commands. You can reuse one of these commands
directly by referring to the number of that command.

For example, if your history looked like this:

~~~
259  ls *
260  ls /usr/bin/*.sh
261  ls *R1*fastq
~~~
{: .output}

then you could repeat command #260 by entering:

~~~
!260
~~~
{: .bash}

Type `!` (exclamation point) and then the number of the command from your history.
You will be glad you learned this when you need to re-run very complicated commands.

> ## Exercise
> Find the line number in your history for the command that listed all the .sh
> files in `/usr/bin`. Rerun that command.
{: .challenge}

## Examining Files

We now know how to switch directories, run programs, and look at the
contents of directories, but how do we look at the contents of files?

One way to examine a file is to print out all of the
contents using the program `cat`. 

Enter the following command from within the `untrimmed_fastq` directory: 

~~~
$ cat SRR098026.fastq
~~~
{: .bash}

This will print out all of the contents of the `SRR098026.fastq` to the screen.


> ## Exercise
> 
> 1. Print out the contents of the `~/dc_sample_data/untrimmed_fastq/SRR097977.fastq` file. What is the last line of the file? 
> 2.  From your home directory, and without changing directories,
> use one short command to print the contents of all of the files in
> the `~/dc_sample_data/untrimmed_fastq` directory.
> 
> > ## Solution
> > 1. The last line of the file is `TATTTTAAAATGGAATACCTAACATGTTAATTAACC`.
> > 2. cat ~/dc_sample_data/untrimmed_fastq/*
> {: .solution}
{: .challenge}

`cat` is a terrific program, but when the file is really big, it can
be annoying to use. The program, `less`, is useful for this
case. `less` opens the file as read only, and lets you navigate through it. The naviation commands
are identical to the `man` program.

Enter the following command:

~~~
$ less SRR098026.fastq
~~~
{: .bash}

Some navigation commands in `less`

| key     | action |
| ------- | ---------- |
| "space" | to go forward |
|  "b"    | to go backwarsd |
|  "g"    | to go to the beginning |
|  "G"    | to go to the end |
|  "q"    | to quit |

`less` also gives you a way of searching through files. Use the
"/" key to begin a search. Enter the word you would like
to search for and press `enter`. The screen will jump to the next location where
that word is found. 

**Shortcut:** If you hit "/" then "enter", `less` will  repeat
the previous search. `less` searches from the current location and
works its way forward. Note, if you are at the end of the file and search
for the word "cat", `less` will not find it. You need to go to the
beginning of the file and search.

For instance, let's search the file we have open for the sequence `GTGCGGGCAATTAACAGGGGTTCAC`.
You can see that we go right to that sequence and can see
what it looks like.

## Exercise
> What are the next three nucleotides (characters) after the sequence quoted above?
> 
> > ## Solution
> > `TCA`
> {: .solution}
{: .challenge}

Remember, the `man` program actually uses `less` internally and
therefore uses the same commands, so you can search documentation
using "/" as well!

There's another way that we can look at files, and in this case, just
look at part of them. This can be particularly useful if we just want
to see the beginning or end of the file, or see how it's formatted.

The commands are `head` and `tail` and they let you look at
the beginning and end of a file, respectively.

    head SRR098026.fastq
    tail SRR098026.fastq

The `-n` option to either of these commands can be used to print the
first or last `n` lines of a file. To print the first/last line of the
file use:

    head -n 1 SRR098026.fastq
    tail -n 1 SRR098026.fastq


## Creating, moving, copying, and removing

Now we can move around in the file structure, look at files, search files,
redirect. But what if we want to do normal things like copy files or move
them around or get rid of them. Sure we could do most of these things
without the command line, but what fun would that be?! Besides it's often
faster to do it at the command line, or you'll be on a remote server
like Amazon where you won't have another option.

### Copying 

Our raw data in this case is fastq files.  We don't want to change the original files,
so let's make a copy to work with.

Lets copy the file using the `cp` command. The `cp`
command backs up the file. 

Navigate to the `data` directory and enter:

    cp SRR098026.fastq SRR098026-copy.fastq
    ls -F
    SRR097977.fastq  SRR098026-copy.fastq  SRR098026.fastq

Now SRR098026-copy.fastq has been created as a copy of SRR098026.fastq

Let's make a `backup` directory where we can put this file.

### Creating Directories

The `mkdir` command is used to make a directory. Just enter `mkdir`
followed by a space, then the directory name.

    mkdir backup

### Moving / Renaming 

We can now move our backed up file in to this directory. We can
move files around using the command `mv`. 

Enter this command:

    mv *-copy.fastq backup
    ls -al backup
    
    total 52
    drwxrwxr-x 2 dcuser dcuser  4096 Jul 30 15:31 .
    drwxr-xr-x 3 dcuser dcuser  4096 Jul 30 15:31 ..
    -rw-r--r-- 1 dcuser dcuser 43421 Jul 30 15:28 SRR098026-copy.fastq

The `mv` command is also how you rename files. Since this file is so
important, let's rename it! 

Type:

    cd backup
    mv SRR098026-copy.fastq SRR098026-copy.fastq_DO_NOT_TOUCH!
    ls
    
    SRR098026-copy.fastq_DO_NOT_TOUCH!

### Removing

Finally, we decided this was silly and want to start over.

Type:

    rm backup/SRR*

The `rm` file permanently removes the file. Be careful with this command. It doesn't
just nicely put the files in the Trash. They're really gone.

By default, `rm`, will NOT delete directories. You can tell `rm` to
delete a directory using the `-r` option. Let's delete that `new` directory
we just made. 

Enter the following command:

    rm -r backup

* * * *
**Exercise**

Do the following:

1.  Create a backup of your SRR097977.fastq file in the directory containing the original file.
2.  Move the backup copy to the backup directory.
3.  Rename the backup copy of your file.

* * * *


