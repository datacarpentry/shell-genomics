---
layout: page
title: "The Shell"
comments: true
date: 2015-07-30
---

# The Shell

Author: Sheldon McKay
Adapted from the lesson by Tracy Teal.
Original contributors:
Paul Wilson, Milad Fatenejad, Sasha Wood and Radhika Khetani for Software Carpentry (http://software-carpentry.org/)

## Searching files

We showed a little how to search within a file using `less`. We can also
search within files without even opening them, using `grep`. Grep is a command-line
utility for searching plain-text data sets for lines matching a string or regular expression.
Let's give it a try!

Suppose we want to see how many reads in our file have really bad, with 10 consecutive Ns  
Let's search for the string NNNNNNNNNN in file 

     grep NNNNNNNNNN SRR098026.fastq

We get back a lot of lines.  What is we want to see the whole fastq record for each of these read.
We can use the '-B' argument for grep to return the matched line plus the three lines before it.
Since each record is four lines and the last line is the sequence, this should give the whole record.

    grep -B3 NNNNNNNNNN SRR098026.fastq

for example:

    +SRR098026.24 HWUSI-EAS1599_1:2:1:0:1009 length=35
    !!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
    @SRR098026.25 HWUSI-EAS1599_1:2:1:0:1027 length=35
    NNNNNNNNNNNNNNNNGNNNNNNNNNNNNNNNNNN


With nice symmetry, the `-A` flag stands for "after match" will return the specified
number of lines after the match.

***
** Exercise **
1) Search for the sequence GNATNACCACTTCC in SRR098026.fastq.
In addition to finding the sequence, have your search also return
the name of the sequence.

2) Serach for that sequence in both fastq files.
***


## Redirection

We're excited we have all these sequences that we care about that we
just got from the FASTQ files. That is a really important motif
that is going to help us answer our important question. But all those
sequences just went whizzing by with grep. How can we capture them?

We can do that with something called "redirection". The idea is that
we're redirecting the output to the terminal (all the stuff that went
whizzing by) to something else. In this case, we want to print it
to a file, so that we can look at it later.

The redirection command for putting something in a file is `>`

Let's try it out and put all the sequences that contain 'TTATCCGGATTTATTGGGTTTAAAGGGT'
from all the files in to another file called 'good-data.txt'

    grep -B 2 TTATCCGGATTTATTGGGTTTAAAGGGT * > good-data.txt

The prompt should sit there a little bit, and then it should look like nothing
happened. But type `ls`. You should have a new file called good-data.txt. Take
a look at it and see if it has what you think it should.

There's one more useful redirection command that we're going to show, and that's
called the pipe command, and it is `|`. It's probably not a key on
your keyboard you use very much. What `|` does is take the output that
scrolling by on the terminal and then can run it through another command.
When it was all whizzing by before, we wished we could just slow it down and
look at it, like we can with `less`. Well it turns out that we can! We pipe
the `grep` command through `less`

    grep TTATCCGGATTTATTGGGTTTAAAGGGT * | less

Now we can use the arrows to scroll up and down and use `q` to get out.

We can also do something tricky and use the command `wc`. `wc` stands for
`word count`. It counts the number of lines or characters. So, we can use
it to count the number of lines we're getting back from our `grep` command.
And that will magically tell us how many sequences we're finding. We're

    grep TTATCCGGATTTATTGGGTTTAAAGGGT * | wc

That tells us the number of lines, words and characters in the file. If we
just want the number of lines, we can use the `-l` flag for `lines`.

    grep TTATCCGGATTTATTGGGTTTAAAGGGT * | wc -l

Redirecting is not super intuitive, but it's really powerful for stringing
together these different commands, so you can do whatever you need to do.

The philosophy behind these command line programs is that none of them
really do anything all that impressive. BUT when you start chaining
them together, you can do some really powerful things really
efficiently. If you want to be proficient at using the shell, you must
learn to become proficient with the pipe and redirection operators:
`|`, `>`, `>>`.


BREAK

## Creating, moving, copying, and removing

Now we can move around in the file structure, look at files, search files,
redirect. But what if we want to do normal things like copy files or move
them around or get rid of them. Sure we could do most of these things
without the command line, but what fun would that be?! Besides it's often
faster to do it at the command line, or you'll be on a remote server
like Amazon where you won't have another option.

The stability.files file is one that tells us what sample name
goes with what sequences. This is a really important file, so
we want to make a copy so we don't lose it.

Lets copy the file using the `cp` command. The `cp`
command backs up the file. Navigate to the `data` directory and enter:

    cp stability.files stability.files_backup

Now `stability.files_backup` has been created as a copy of `stability.files`.

Let's make a `backup` directory where we can put this file.

The `mkdir` command is used to make a directory. Just enter `mkdir`
followed by a space, then the directory name.

    mkdir backup

We can now move our backed up file in to this directory. We can
move files around using the command `mv`. Enter this command:

    mv stability.files_backup backup/

This moves `stability.files_backup` into the directory `backup/` or
the full path would be `~/edamame-data/shell/MiSeq/backup`

The `mv` command is also how you rename files. Since this file is so
important, let's rename it:

    mv stability.files stability.files_IMPORTANT

Now the file name has been changed to stability.files_IMPORTANT. Let's delete
the backup file now:

    rm backup/stability.files_backup

The `rm` file removes the file. Be careful with this command. It doesn't
just nicely put the files in the Trash. They're really gone.



* * * *
**Exercise**

Do the following:

1.  Rename the `stability.files_IMPORTANT` file to `stability.files`.
2.  Create a directory in the `MiSeq` directory called `new`
3.  Then, copy the `stability.files` file into `new`

* * * *

By default, `rm`, will NOT delete directories. You can tell `rm` to
delete a directory using the `-r` option. Let's delete that `new` directory
we just made. Enter the following command:

    rm -r new

## Writing files

We've been able to do a lot of work with files that already exist, but what
if we want to write our own files. Obviously, we're not going to type in
a FASTA file, but you'll see as we go through other tutorials, there are
a lot of reasons we'll want to write a file, or edit an existing file.

To write in files, we're going to use the program `nano`. We're going to create
a file that contains the favorite grep command so you can remember it for later. We'll name this file
'awesome.sh'.

    nano awesome.sh

Now you have something that looks like

![nano1.png](img/nano1.png)

Type in your command, so it looks like

![nano2.png](img/nano2.png)

Now we want to save the file and exit. At the bottom of nano, you see the "^X Exit". That
means that we use Ctrl-X to exit. Type `Ctrl-X`. It will ask if you want to save it. Type `y` for yes.
Then it asks if you want that file name. Hit 'Enter'.

Now you've written a file. You can take a look at it with less or cat, or open it up again and edit it.

***
**Exercise**

Open 'awesome.sh' and add "echo AWESOME!" after the grep command and save the file.

We're going to come back and use this file in just a bit.

***


## Running programs

Commands like `ls`, `rm`, `echo`, and `cd` are just ordinary programs
on the computer. A program is just a file that you can *execute*. The
program `which` tells you the location of a particular program. For
example:

    which ls

Will return "/bin/ls". Thus, we can see that `ls` is a program that
sits inside of the `/bin` directory. Now enter:

    which find

You will see that `find` is a program that sits inside of the
`/usr/bin` directory.

So ... when we enter a program name, like `ls`, and hit enter, how
does the shell know where to look for that program? How does it know
to run `/bin/ls` when we enter `ls`. The answer is that when we enter
a program name and hit enter, there are a few standard places that the
shell automatically looks. If it can't find the program in any of
those places, it will print an error saying "command not found". Enter
the command:

    echo $PATH

This will print out the value of the `PATH` environment variable. More
on environment variables later. Notice that a list of directories,
separated by colon characters, is listed. These are the places the
shell looks for programs to run. If your program is not in this list,
then an error is printed. The shell ONLY checks in the places listed
in the `PATH` environment variable.

Navigate to the `shell` directory and list the contents. You will
notice that there is a program (executable file) called `hello.sh` in
this directory. Now, try to run the program by entering:

    hello.sh

You should get an error saying that hello.sh cannot be found. That is
because the directory `/home/dcuser/dc_sample_data/data` is not in the
`PATH`. You can run the `hello.sh` program by entering:

    ./hello.sh

Remember that `.` is a shortcut for the current working
directory. This tells the shell to run the `hello.sh` program which is
located right here. So, you can run any program by entering the path
to that program. You can run `hello.sh` equally well by specifying:

    /home/dcuser/dc_sample_data/data/hello.sh

Or by entering:

    ~/dc_sample_data/data/hello.sh

When there are no `/` characters, the shell assumes you want to look
in one of the default places for the program.

## Writing scripts

We know how to write files and run scripts, so I bet you can guess where
this is headed. We're going to run our own script!

Go in to the 'MiSeq' directory where we created 'awesome.sh' before. Remember we wrote our
favorite grep command in there. Since we like it so much, we might want to run it
again, or even all the time. Instead of writing it out every time, we can just run it as
a script.

It's a command, so we should just be able to run it. Give it try.

    ./awesome.sh

Alas, we get `-bash: ./awesome.sh: Permission denied`. This is because we haven't told
the computer that it's a program. To do that we have to make it 'executable'. We do this
by changing its mode. The command for that is `chmod` - change mode. We're going to change the mode
of this file, so that it's executable and the computer knows it's OK to run it as a program.

    chmod +x awesome.sh

Now let's try running it again

    ./awesome.sh

Now you should have seen some output, and of course, it's AWESOME!
Congratulations, you just created your first shell script! You're set to rule the world.

## Bonus materials: Automation

Looping at the command line

Example: Something you might want to do fairly often is to change the name of a lot of files.
You can do that with a 'for' loop.

The syntax for that is in the shell is

   for variable in set-of-things;
       do something on $variable;
       done

A standard variable people use is `i`, but you can use any letter or word you want

So, for instance, let's list all the FASTQ files

      for i in *.fastq;
        do echo $i;
        done

Or if we just wanted to look at the first 20 lines of each of the .fastq files, we could do

     for i in *.fastq;
        head -n 40 $i;
        done

If we wanted to output these first 40 lines to a new file, we could do

     for i in #.fastq;
         head -n 40 $i > new_$i;
         done

***
**Bonus exercise**
Rename the stability files to have a .txt extension

***

Example of renaming files with a different extension. Changing `fastq` to `fq`

    for i in *.fastq;
         do mv "$i" "${i/%.fastq/.fq}";
         done


# For Future Reference

# Finding files

The `find` program can be used to find files based on arbitrary
criteria. Navigate to the `data` directory and enter the following
command:

    find . -print

This prints the name of every file or directory, recursively, starting
from the current directory. Let's exclude all of the directories:

    find . -type f -print

This tells `find` to locate only files. Now try these commands:

    find . -type f -name "*1*"
    find . -type f -name "*1*" -or -name "*2*" -print
    find . -type f -name "*1*" -and -name "*2*" -print

The `find` command can acquire a list of files and perform some
operation on each file. Try this command out:

    find . -type f -exec grep Volume {} \;

This command finds every file starting from `.`. Then it searches each
file for a line which contains the word "Volume". The `{}` refers to
the name of each file. The trailing `\;` is used to terminate the
command.  This command is slow, because it is calling a new instance
of `grep` for each item the `find` returns.

A faster way to do this is to use the `xargs` command:

    find . -type f -print | xargs grep Volume

`find` generates a list of all the files we are interested in,
then we pipe them to `xargs`.  `xargs` takes the items given to it
and passes them as arguments to `grep`.  `xargs` generally only creates
a single instance of `grep` (or whatever program it is running).



## Where can I learn more about the shell?

- Software Carpentry tutorial - [The Unix shell](http://software-carpentry.org/v4/shell/index.html)
- The shell handout - [Command Reference](http://files.fosswire.com/2007/08/fwunixref.pdf)
- [explainshell.com](http://explainshell.com)
- http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html
- man bash
- Google - if you don't know how to do something, try Googling it. Other people
have probably had the same question.
- Learn by doing. There's no real other way to learn this than by trying it
out.  Write your next paper in nano (really emacs or vi), open pdfs from
the command line, automate something you don't really need to automate.


## Bonus:

**backtick, xargs**: Example find all files with certain text

**alias** -> rm -i

**variables** -> use a path example

**.bashrc**

**du**

**ln**

**ssh and scp**

**Regular Expressions**

**Permissions**

**Chaining commands together**
