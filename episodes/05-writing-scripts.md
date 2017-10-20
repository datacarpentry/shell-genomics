---
title: "Writing Scripts"
teaching: 0
exercises: 0
questions:
- How can we easily execute a commonly used set of commands.
objectives:
- Use the nano text editor to modify text files.
- Write a basic shell script
- Use the bash command to execute a shell script.
- Use chmod to make a script an executable program.
keypoints:
- Scripts are a collection of commands executed together
---

## Writing files

We've been able to do a lot of work with files that already exist, but what if we want to write our own files. Obviously, we're not going to type in a FASTA file, but we'll see as we go through other tutorials, there area lot of reasons we'll want to write a file, or edit an existing file.

To write in files, we're going to use the program `nano`. We're going to create a file to take notes on what we've been doing with the data files in `~/dc_sample_data/untrimmed_fastq`.

This is good practice when working in bioinformatics. We can create a file called a `README.txt` that describes the data files in the directory or documents how the files in that directory were generated.  As the name suggests it's a file that we or others should read to understand the information in that directory.

First go into this directory.

~~~
$ cd ~/dc_sample_data/untrimmed_fastq
~~~
{: .bash}

Now we're going to create this file

~~~
$ nano README.txt
~~~
{: .bash}

Now you have something that looks like

![nano1.png](../img/nano1.png)

In this file you can type whatever you want. Describe what the files in this
directory are or what you've been doing with them.

Now we want to save the file and exit. At the bottom of nano, you see the `^X Exit`. That means that we use `Ctrl-X` to exit. Type `Ctrl-X`. It will ask if you want to save it. Type `y` for yes. Then it asks if you want that file name. Hit `Enter`.

Now you've written a file. You can take a look at it with `less` or `cat`, or open it up again and edit it with `nano`.

> ## Exercise
>
> Open `README.txt` and add the date to the top of the file and save the file.
{: .challenge}

## Writing scripts

A really powerful thing about the command line is that you can write scripts. Scripts let you save commands to run them and also lets you put multiple commands together. In the 'winning' plot, this is where you win, because you are automating your work.

![Automation](../img/gvng.jpg)

We're generating new sequences all the time, and we want to be able to pull out the bad reads and write them to a file to see if we can figure out what's going on with them. So, we're going to look for reads with long sequences of N's like we did before, but we want to write a script, so we can just run it each time we get new sequences.

Bad reads have a lot of N's, so we're going to look for  `NNNNNNNNNN` with `grep`. We want the whole FASTQ record, so we're also going to get the 1 line above the sequence and the two lines below. We also want to look in all the files that end with fastq, so we're going to use the `*` wild card.

~~~
$ grep -B1 -A2 NNNNNNNNNN *.fastq > scripted_bad_reads.txt
~~~
{: .bash}

We're going to create a new file to put this command in. We'll call it `bad-reads-script.sh`. The `sh` isn't required, but using that extension tells us that it's a shell script.

~~~
$ nano bad-reads-script.sh
~~~
{: .bash}

Type your `grep` command into the file and save it as before.

Now comes the neat part. We can run this script. Type:

~~~
$ bash bad-reads-script.sh
~~~
{: .bash}

It will look like nothing happened, but now if you look at `scripted_bad_reads.txt`, you can see that there are reads in there.

> ## Exercise
>
> We want the script to tell us when it's done.
> 1. Open `bad-reads-script.sh` and add the line `echo "Script finished!"` after the `grep` command and save the file.
> 2. Run the updated script.
{: .challenge}

## Making the script into a program

We had to type `bash` because we needed to tell the computer what program to use to run this script. Instead we can turn this script into its own program. We need to tell it that it's a program by making it executable. We can do this by changing the file permissions. We
talked about permissions in [an earlier episode](http://www.datacarpentry.org/shell-genomics/03-working-with-files/).

First, let's look at the current permissions.

~~~
$ ls -l bad-reads-script.sh
~~~
{: .bash}

We see that it says `-rw-r--r--`. This shows that the file can be read by any user and written to by the file owner (you). We want to change these permissions so that the file can be executed as a program. We use the command `chmod` like we did earlier when we removed write permissions. Here we are adding (`+`) executable permissions (`+x`).

~~~
$ chmod +x bad-reads-script.sh
~~~
{: .bash}

Now let's look at the permissions again.

~~~
$ ls -l bad-reads-script.sh
~~~
{: .bash}

Now we see that it says `-rwxr-xr-x`. The `x`'s that are there now tell us we can run it as a program. So, let's try it! We'll need to put `./` at the beginning so the computer knows to look here in this directory for the program.

~~~
$ ./bad-reads-script.sh
~~~
{: .bash}

The script should run the same way as before, but now we've created our very own computer program!

We'll have a chance to do more of this as we go through bioinformatics pipelines.

## Where can I learn more about the shell?

- Software Carpentry tutorial - [The Unix shell](https://swcarpentry.github.io/shell-novice/reference/)
- The shell handout - [Command Reference](http://files.fosswire.com/2007/08/fwunixref.pdf)
- [explainshell.com](http://explainshell.com)
- http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html
- man bash
- Google - if you don't know how to do something, try Googling it. Other people
have probably had the same question.
- Learn by doing. There's no real other way to learn this than by trying it
out.  Write your next paper in nano (really emacs or vi), open pdfs from
the command line, automate something you don't really need to automate.
