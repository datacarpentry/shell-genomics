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

2) Search for that sequence in both fastq files.
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

    grep -B3 NNNNNNNNNN SRR098026.fastq > bad_reads.txt

The prompt should sit there a little bit, and then it should look like nothing
happened. But type `ls`. You should have a new file called good-data.txt. Take
a look at it and see if it has what you think it should.

If we use '>>', it will append to rather tha overwrite a file.  This can be useful for
saving more than one search, for example:

    grep -B3 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
    grep -B3 NNNNNNNNNN SRR097977.fastq >> bad_reads.txt

There's one more useful redirection command that we're going to show, and that's
called the pipe command, and it is `|`. It's probably not a key on
your keyboard you use very much. What `|` does is take the output that
scrolling by on the terminal and then can run it through another command.
When it was all whizzing by before, we wished we could just slow it down and
look at it, like we can with `less`. Well it turns out that we can! We pipe
the `grep` command through `less`

    grep -B3 NNNNNNNNNN SRR098026.fastq | less

Now we can use the arrows to scroll up and down and use `q` to get out.

We can also do something tricky and use the command `wc`. `wc` stands for
`word count`. It counts the number of lines or characters. So, we can use
it to count the number of lines we're getting back from our `grep` command.
And that will magically tell us how many sequences we're finding. We're

    grep -B3 NNNNNNNNNN SRR098026.fastq | wc

That tells us the number of lines, words and characters in the file. If we
just want the number of lines, we can use the `-l` flag for `lines`.

    grep -B3 NNNNNNNNNN SRR098026.fastq | wc -l

Redirecting is not super intuitive, but it's really powerful for stringing
together these different commands, so you can do whatever you need to do.

The philosophy behind these command line programs is that none of them
really do anything all that impressive. BUT when you start chaining
them together, you can do some really powerful things really
efficiently. If you want to be proficient at using the shell, you must
learn to become proficient with the pipe and redirection operators:
`|`, `>`, `>>`.











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
