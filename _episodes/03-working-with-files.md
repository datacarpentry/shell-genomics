---
title: "Working with Files"
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

## Working with Files

### Our data set: FASTQ files

We did an experiment and want to look at sequencing results.
We want to be able to look at these files and do some things with them.


### Wild cards

Navigate to the `~/dc_sample_data/data/untrimmed_fastq` directory. This
directory contains our FASTQ files.

The `*` character is a shortcut for "everything". Thus, if
you enter `ls *`, you will see all of the contents of a given
directory.

Now try this command:

    ls *fastq

This lists every file that ends with a `fastq`.

This command:

    ls /usr/bin/*.sh

Lists every file in `/usr/bin` that ends in the characters `.sh`.

    ls *977.fastq

lists only the file that ends with `977.fastq`

So how does this actually work? Well...when the shell (bash) sees a
word that contains the `*` character, it automatically looks for filenames
that match the given pattern.

We can use the command `echo` to see wilcards are they are intepreted by the shell.

    echo *.fastq
    SRR097977.fastq SRR098026.fastq

The `*` is expanded to include any file that ends with `.fastq`.


****
**Exercise**

Do each of the following using a single `ls` command without
navigating to a different directory.

1.  List all of the files in `/bin` that start with the letter 'c'
2.  List all of the files in `/bin` that contain the letter 'a'
3.  List all of the files in `/bin` that end with the letter 'o'

BONUS: List all of the files in '/bin' that contain the letter 'a' or 'c'

****


## Command History

You can easily access previous commands.  Hit the up arrow.
Hit it again.  You can step backwards through your command history.
The down arrow takes your forwards in the command history.

`^-C` will cancel the command you are writing, and give you a fresh prompt.

`^-R` will do a reverse-search through your command history.  This
is very useful.

You can also review your recent commands with the `history` command.  Just enter:

    history

to see a numbered list of recent commands, including this just issues
`history` command.  You can reuse one of these commands directly by
referring to the number of that command.

If your history looked like this:

    259  ls *
    260  ls /usr/bin/*.sh
    261  ls *R1*fastq

then you could repeat command #260 by simply entering:

    !260

(that's an exclamation mark).  You will be glad you learned this when you try to re-run very complicated commands.

****
**Exercise**

1. Find the line number in your history for the last exercise (listing
files in /bin) and reissue that command.

****



## Examining Files

We now know how to switch directories, run programs, and look at the
contents of directories, but how do we look at the contents of files?

The easiest way to examine a file is to just print out all of the
contents using the program `cat`. 

Enter the following command:

    cat SRR098026.fastq

This prints out the all the contents of the the `SRR098026.fastq` to the screen.

* * * *
**Exercises**

1.  Print out the contents of the `~/dc_sample_data/untrimmed_fastq/SRR097977.fastq`
    file. What does this file contain?

2.  From your home directory, without changing directories,
    use one short command to print the contents of all of the files in
    the `/home/dcuser/dc_sample_data/untrimmed_fastq` directory.

* * * *


    cd ~/dc_sample_data/untrimmed_fastq

`cat` is a terrific program, but when the file is really big, it can
be annoying to use. The program, `less`, is useful for this
case. 

Enter the following command:

    less SRR098026.fastq

`less` opens the file as read only, and lets you navigate through it. The naviation commands
are identical to the `man` program.

**Some navigation commands in `less`**

| key     | action |
| ------- | ---------- |
| "space" | to go forward |
|  "b"    | to go backwarsd |
|  "g"    | to go to the beginning |
|  "G"    | to go to the end |
|  "q"    | to quit |

`less` also gives you a way of searching through files. Just hit the
"/" key to begin a search. Enter the word you would like
to search for and press "enter". The screen will jump to the next location where
that word is found. Try searching the `dictionary.txt` file for the
word "cat". 
**Shortcut:** If you hit "/" then "enter", `less` will  repeat
the previous search. `less` searches from the current location and
works its way forward. Note, if you are at the end of the file and search
for the word "cat", `less` will not find it. You need to go to the
beginning of the file and search.

For instance, let's search for the sequence `GTGCGGGCAATTAACAGGGGTTCAC` in our file.
You can see that we go right to that sequence and can see
what it looks like.

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

1.  Create a backup of your fastq files.
2.  Create a backup directory.
3.  Copy a backup of your files there.

* * * *


