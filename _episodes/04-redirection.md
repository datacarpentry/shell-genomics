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

We discussed in a previous episode how to search within a file using `less`. We can also
search within files without even opening them, using `grep`. Grep is a command-line
utility for searching plain-text files for lines matching a specific set of 
characters (sometimes called a string) or a particular pattern 
(which can be specified using something called regular expressions). We're not going to work with 
regular expressions in this lesson, and are instead going to specify the strings 
we are searching for.
Let's give it a try!

Suppose we want to see how many reads in our file have really bad segments containing 10 consecutive unknown nucleoties (Ns).  
Let's search for the string NNNNNNNNNN in the SRR098026 file.

~~~
$ grep NNNNNNNNNN SRR098026.fastq
~~~
{: .bash}

This command returns a lot of output to the terminal. Each line in the SRR098026 
file which contains at least 10 consecutive Ns is printed to the terminal. We may be 
interested not only in the actual sequence which contains this string, but 
in the name (or identifier) of that sequence. We discussed in a previous lesson 
that the identifier line immediately precedes the nucleotide sequence for each read
in a FASTQ file. We may also want to inspect the quality scores associated with
each of these reads. To get all of this information, we will return the line 
immediately before each match and the two lines immediately after each match.

We can use the `-B` argument for grep to return a specific number of lines before
each match and the `-A` argument to return a specific number of lines after each matching line. Here we want the line before and the two lines after each 
matching line so we add `-B1 -A2` to our grep command.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq
~~~
{: .bash}

One of the sets of lines returned by this command is: 

~~~
@SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
CNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
+SRR098026.177 HWUSI-EAS1599_1:2:1:1:2025 length=35
#!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
~~~
{: .output}

> ## Exercise
>
> 1) Search for the sequence GNATNACCACTTCC in the SRR098026.fastq.
> Have your search return all matching lines and the name (or identifier) for each sequence
> that contains a match.
> 
> 2) Search for the sequence AAGTT in both FASTQ files.
> Have your search return all matching lines and the name (or identifier) for each sequence
> that contains a match.
{: .challenge}

## Redirection

`grep` allowed us to identify sequences in our FASTQ files that match a particular pattern. 
But all of these sequences were printed to our terminal screen. In order to work with these 
sequences and perform other opperations on them, we will need to capture that output in some
way. 

We can do this with something called "redirection". The idea is that
we're redirecting what was output to the terminal to another location. 
In our case, we want to print this information to a file, so that we can look at it later and 
do other analyses with this data.

The command for redirecting output to a file is `>`.

Let's try out this command and copy all the records (including all four lines of each record) 
in our FASTQ files that contain 
'NNNNNNNNNN' to another file called 'bad_reads.txt'.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
~~~
{: .bash}

The prompt should sit there a little bit, and then it should look like nothing
happened. But type `ls`. You should see a new file called bad_reads.txt. 

We can check the number of lines in our new file using a command called `wc`. 
`wc` stands for `word count`. This command counts the number of words, lines, and characters
in a file. 

~~~
$ wc bad_reads.txt
~~~
{: .bash}

This will tell us the number of lines, words and characters in the file. If we
want only the number of lines, we can use the `-l` flag for `lines`.

~~~
$ wc -l bad_reads.txt
~~~
{: .bash}

Because we asked `grep` for all four lines of each FASTQ record, we need to divide the output by
four to get the number of sequences that match our search pattern.

> ## Exercise
>
> How many sequences in SRR098026.fastq contain at least 3 consecutive Ns?
>
>> ## Solution
>> 
> {: .solution}
{: .challenge}

We might want to search multiple FASTQ files for sequences that match our search pattern.
However, we need to be careful, because each time we use the `>` command to redirect output
to a file, the new output will replace the output that was already present in the file. 
This is called "overwriting" and, just like you don't want to overwrite your video recording
of your kid's first birthday party, you also want to avoid overwriting your data files.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
$ wc -l bad_reads.txt
$ grep -B1 -A2 NNNNNNNNNN SRR097977.fastq > bad_reads.txt
$ wc -l bad_reads.txt
~~~
{: .bash}

Here, the output of our second  call to `wc` shows that we no longer have any lines in our bad_reads.txt file. This is 
because the second file we searched (SRR097977.fastq) does not contain any lines that match our
search sequence. So our file was overwritten and is now empty.

We can avoid overwriting our files by using the command `>>`. `>>` will 
append new output to the end of a file, rather than overwriting it.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt
$ wc -l bad_reads.txt
$ grep -B1 -A2 NNNNNNNNNN SRR097977.fastq >> bad_reads.txt
$ wc -l bad_reads.txt
~~~
{: .bash}

The output of our second call to `wc` shows that we have not overwritten our original data. 

We can also do this with a single line of code by using a wildcard. 

~~~
$ grep -B1 -A2 NNNNNNNNNN *.fastq > bad_reads.txt
~~~
{: .bash}

> ## Exercise
>
> 
>
>> ## Solution
>> 
> {: .solution}
{: .challenge}


There's one more useful redirection command that we're going to show, and that's
called the pipe command (`|`). This is probably not a key on
your keyboard you use very much, so let's all take a minute to find that key. 
What `|` does is take the output that is
scrolling by on the terminal and uses that output as input to another command. 
When our output was scrolling by, we might have wished we could slow it down and
look at it, like we can with `less`. Well it turns out that we can! We can redirect our output
from our `grep` call through the `less` command.

~~~
$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq | less
~~~
{: .bash}

We can now see the output from our `grep` call within the `less` interface. We can use the up and down arrows 
to scroll through the output and use `q` to exit `less`.

Redirecting output is often not intuitive, and can take some time to get used to. Once you're 
comfortable with redirection, however, you'll be able to combine any number of commands to
do all sorts of exciting things with your data!

None of the command line programs we've been learning
do anything all that impressive on their own, but when you start chaining
them together, you can do some really powerful things very
efficiently. Let's take a few minutes to practice. 

> ## Exercise
>
> 
>
>> ## Solution
>> 
> {: .solution}
{: .challenge}

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
