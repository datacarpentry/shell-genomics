---
title: "Redirection"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- Employ the grep command to search for information within files.
- Print the results of a command to a file.
- Access resources to learn more information about the shell.
keypoints:
- "First key point."
---

## Searching files

We showed a little how to search within a file using `less`. We can also
search within files without even opening them, using `grep`. Grep is a command-line
utility for searching plain-text data sets for lines matching a string or regular expression.
Let's give it a try!

Suppose we want to see how many reads in our file have really bad segments containing 10 consecutive Ns.  
Let's search for the string NNNNNNNNNN in the SRR098026 file.

~~~
$ grep NNNNNNNNNN SRR098026.fastq
~~~
{: .bash}

We get back a lot of lines. What we want to see is the whole fastq record for each of these reads. The fastq record consists of one line before the sequence information as well as two lines after. We can use the '-B' argument for grep to return the matched line plus one before: '-B1'. With the '-A argument', we can have grep list the two lines after also: '-A2'.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq
~~~
{: .bash}

for example:

~~~
@SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
CNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
+SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
~~~
{: .output}

> ## Exercise
>
> 1) Search for the sequence GNATNACCACTTCC in SRR098026.fastq.
> In addition to identifying the line containing the sequence, have your search also return
> the line containing the name of the sequence (tip: the name of the sequence is listed after the '@' sign).
> 
> 2) Search for the sequence AAGTT in both fastq files. Get the lines containing the name of the sequence and the sequence itself.
{: .challenge}

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

Let's try it out and put all the sequences that contain 'NNNNNNNNNN'
from all the files in to another file called 'bad_reads.txt'

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
~~~
{: .bash}

The prompt should sit there a little bit, and then it should look like nothing
happened. But type `ls`. You should have a new file called bad_reads.txt. Take
a look at it and see if it has what you think it should.

If we use `>>`, it will append to rather than overwrite a file.  This can be useful for
saving more than one search, for example:

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
$ grep -B1 -A2 NNNNNNNNNN SRR097977.fastq >> bad_reads.txt
~~~
{: .bash}

There's one more useful redirection command that we're going to show, and that's
called the pipe command, and it is `|`. It's probably not a key on
your keyboard you use very much. What `|` does is take the output that
scrolling by on the terminal and then can run it through another command.
When it was all whizzing by before, we wished we could just slow it down and
look at it, like we can with `less`. Well it turns out that we can! We pipe
the `grep` command through `less`.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq | less
~~~
{: .bash}

Now we can use the arrows to scroll up and down and use `q` to get out.

We can also do something tricky and use the command `wc`. `wc` stands for `word count`. It counts the number of lines or characters. So, we can use it to count the number of lines we're getting back from our `grep` command. If we divide by it four (to account for the additional three lines we've requested) that will magically tell us how many sequences we're finding.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq | wc
~~~
{: .bash}

That tells us the number of lines, words and characters in the file. If we
just want the number of lines, we can use the `-l` flag for `lines`.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq | wc -l
~~~
{: .bash}

Redirecting is not super intuitive, but it's really powerful for stringing
together these different commands, so you can do whatever you need to do.

The philosophy behind these command line programs is that none of them
really do anything all that impressive. BUT when you start chaining
them together, you can do some really powerful things really
efficiently. If you want to be proficient at using the shell, you must
learn to become proficient with the pipe and redirection operators:
`|`, `>`, `>>`.

Finally, let's use the new tools in our kit and a few new ones to example our SRA metadata file.

~~~
$ cd
$ cd dc_sample_data/sra_metadata
~~~
{: .bash}

Let's ask a few questions about the data.

#### How many of the read libraries are paired end?

We know this information is somewhere in our SraRunTable.txt file, we just need to find it. First, let's look at the column headers.

~~~
$ head -n 1 SraRunTable.txt
~~~
{: .bash}

~~~
BioSample_s	InsertSize_l	LibraryLayout_s	Library_Name_s	LoadDate_s	MBases_l	MBytes_l	ReleaseDate_s Run_s SRA_Sample_s Sample_Name_s Assay_Type_s AssemblyName_s BioProject_s Center_Name_s Consent_s Organism_Platform_s SRA_Study_s g1k_analysis_group_s g1k_pop_code_s source_s strain_s
~~~
{: .output}

That's only the first line but it is a lot to take in.  `cut` is a program that will extract columns in tab-delimited
files.  It is a very good command to know.  Lets look at just the first four columns in the header using the `|` redirect
and `cut`.

~~~
$ head -n 1 SraRunTable.txt | cut -f1-4
~~~
{: .bash}

~~~
BioSample_s InsertSize_l      LibraryLayout_s	Library_Name_s    
~~~
{: .output}

`-f1-4` means to cut the first four fields (columns).  The LibraryLayout_s column looks promising.  Let's look at some data for just that column.

~~~
$ cut -f3 SraRunTable.txt | head -n 10
~~~
{: .bash}

~~~
LibraryLayout_s
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
SINGLE
PAIRED
~~~
{: .output}

We can see that there are (at least) two categories, SINGLE and PAIRED.  We want to search all entries in this column
for just PAIRED and count the number of hits.

~~~
$ cut -f3 SraRunTable.txt | grep PAIRED | wc -l
~~~
{: .bash}

~~~
2
~~~
{: .output}

#### How many of each class of library layout are there?  

We can use some new tools `sort` and `uniq` to extract more information.  For example, cut the third column, remove the
header and sort the values.  The `-v` option for grep means return all lines that DO NOT match.

~~~
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort
~~~
{: .bash}

This returns a sorted list (too long to show here) of PAIRED and SINGLE values.  Now we can use `uniq` with the `-c` flag to
count the different categories.

~~~
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq -c
~~~
{: .bash}

~~~
2 PAIRED
35 SINGLE
~~~
{: .output}

#### Can we sort the file by PAIRED/SINGLE and save it to a new file?  

   We can use the `-k` option for sort to specify which column to sort on.  Note that this does something
   similar to cut's `-f` option.

~~~
$ sort -k3 SraRunTable.txt > SraRunTable_sorted_by_layout.txt
~~~
{: .bash}

#### Can we extract only paired end records into a new file?  

   Do we know PAIRED only occurs in column 4?  We know there are only two in the file, so let's check.

~~~
$ grep PAIRED SraRunTable.txt | wc -l
~~~
{: .bash}

~~~
2
~~~
{: .output}

OK, we are good to go.

~~~
$ grep PAIRED SraRunTable.txt > SraRunTable_only_paired_end.txt
~~~
{: .bash}

> ## Exercise
>
> 1) How many sample load dates are there?
> 2) How many samples were loaded on each date?
> 3) Filter subsets into new files based on load date.
{: .challenge}
