---
title: File manipulation
---

## File manipulation and more practice with pipes

Let's use the tools we've added to our tool kit so far, along with a few new ones, to example our SRA metadata file. First, let's navigate to the correct directory.

```bash
$ cd
$ cd shell_data/sra_metadata
```

This file contains a lot of information about the samples that we submitted for sequencing. We
took a look at this file in an earlier lesson. Here we're going to use the information in this
file to answer some questions about our samples.

#### How many of the read libraries are paired end?

The samples that we submitted to the sequencing facility were a mix of single and paired end
libraries. We know that we recorded information in our metadata table about which samples used
which library preparation method, but we don't remember exactly where this data is recorded.
Let's start by looking at our column headers to see which column might have this information. Our
column headers are in the first row of our data table, so we can use `head` with a `-n` flag to
look at just the first row of the file.

```bash
$ head -n 1 SraRunTable.txt
```

```output
BioSample_s	InsertSize_l	LibraryLayout_s	Library_Name_s	LoadDate_s	MBases_l	MBytes_l	ReleaseDate_s Run_s SRA_Sample_s Sample_Name_s Assay_Type_s AssemblyName_s BioProject_s Center_Name_s Consent_s Organism_Platform_s SRA_Study_s g1k_analysis_group_s g1k_pop_code_s source_s strain_s
```

That is only the first line of our file, but because there are a lot of columns, the output
likely wraps around your terminal window and appears as multiple lines. Once we figure out which
column our data is in, we can use a command called `cut` to extract the column of interest.

Because this is pretty hard to read, we can look at just a few column header names at a time by combining the `|` redirect and `cut`.

```bash
$ head -n 1 SraRunTable.txt | cut -f1-4
```

`cut` takes a `-f` flag, which stands for "field". This flag accepts a list of field numbers,
in our case, column numbers. Here we are extracting the first four column names.

```output
BioSample_s InsertSize_l      LibraryLayout_s	Library_Name_s    
```

The LibraryLayout\_s column looks like it should have the information we want.  Let's look at some
of the data from that column. We can use `cut` to extract only the 3rd column from the file and
then use the `|` operator with `head` to look at just the first few lines of data in that column.

```bash
$ cut -f3 SraRunTable.txt | head -n 10
```

```output
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
```

We can see that there are (at least) two categories, SINGLE and PAIRED.  We want to search all entries in this column
for just PAIRED and count the number of matches. For this, we will use the `|` operator twice
to combine `cut` (to extract the column we want), `grep` (to find matches) and `wc` (to count matches).

```bash
$ cut -f3 SraRunTable.txt | grep PAIRED | wc -l
```

```output
2
```

We can see from this that we have only two paired-end libraries in the samples we submitted for
sequencing.

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise

How many single-end libraries are in our samples?

:::::::::::::::  solution

## Solution

```bash
$ cut -f3 SraRunTable.txt | grep SINGLE | wc -l
```

```output
35
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

#### How many of each class of library layout are there?

We can extract even more information from our metadata table if we add in some new tools: `sort` and `uniq`. The `sort` command will sort the lines of a text file and the `uniq` command will
filter out repeated neighboring lines in a file. You might expect `uniq` to
extract all of the unique lines in a file. This isn't what it does, however, for reasons
involving computer memory and speed. If we want to extract all unique lines, we
can do so by combining `uniq` with `sort`. We'll see how to do this soon.

For example, if we want to know how many samples of each library type are recorded in our table,
we can extract the third column (with `cut`), and pipe that output into `sort`.

```bash
$ cut -f3 SraRunTable.txt | sort
```

If you look closely, you might see that we have one line that reads "LibraryLayout\_s". This is the
header of our column. We can discard this information using the `-v` flag in `grep`, which means
return all the lines that **do not** match the search pattern.

```bash
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort
```

This command returns a sorted list (too long to show here) of PAIRED and SINGLE values. We can use
the `uniq` command to see a list of all the different categories that are present. If we do this,
we see that the only two types of libraries we have present are labelled PAIRED and SINGLE. There
aren't any other types in our file.

```bash
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq
```

```output
PAIRED
SINGLE
```

If we want to count how many of each we have, we can use the `-c` (count) flag for `uniq`.

```bash
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq -c
```

```output
2 PAIRED
35 SINGLE
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise

1. How many different sample load dates are there?
2. How many samples were loaded on each date?

:::::::::::::::  solution

## Solution

1. There are two different sample load dates.
  
  ```bash
  cut -f5 SraRunTable.txt | grep -v LoadDate_s | sort | uniq
  ```
  
  ```output
  25-Jul-12
  29-May-14
  ```

2. Six samples were loaded on one date and 31 were loaded on the other.
  
  ```bash
  cut -f5 SraRunTable.txt | grep -v LoadDate_s | sort | uniq -c
  ```
  
  ```output
   6 25-Jul-12
  31 29-May-14
  ```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

#### Can we sort the file by library layout and save that sorted information to a new file?

We might want to re-order our entire metadata table so that all of the paired-end samples appear
together and all of the single-end samples appear together. We can use the `-k` (key) flag for `sort` to
sort based on a particular column. This is similar to the `-f` flag for `cut`.

Let's sort based on the third column (`-k3`) and redirect our output to a new file.

```bash
$ sort -k3 SraRunTable.txt > SraRunTable_sorted_by_layout.txt
```

#### Can we extract only paired-end records into a new file?

We also might want to extract the information for all samples that meet a specific criterion
(for example, are paired-end) and put those lines of our table in a new file. First, we need
to check to make sure that the pattern we're searching for ("PAIRED") only appears in the column
where we expect it to occur (column 3). We know from earlier that there are only two paired-end
samples in the file, so we can `grep` for "PAIRED" and see how many results we get.

```bash
$ grep PAIRED SraRunTable.txt | wc -l
```

```output
2
```

There are only two results, so we can use "PAIRED" as our search term to extract the paired-end
samples to a new file.

```bash
$ grep PAIRED SraRunTable.txt > SraRunTable_only_paired_end.txt
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise

Sort samples by load date and export each of those sets to a new file (one new file per
unique load date).

:::::::::::::::  solution

## Solution

```bash
$ grep 25-Jul-12 SraRunTable.txt > SraRunTable_25-Jul-12.txt
$ grep 29-May-14 SraRunTable.txt > SraRunTable_29-May-14.txt
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Making code more customizeable using command line arguments

In Lesson 05 (Writing Scripts) we used the `grep` command line tool to look for FASTQ records with
lots of Ns from all the .fastq files in our current folder using the following code:

```bash
$ grep -B1 -A2 -h NNNNNNNNNN *.fastq | grep -v '^--' > scripted_bad_reads.txt
```

This is very useful, but could be more customizeable. We may want to be able to run this command
over and over again without needing to copy and paste it and allow the user to specify exactly which
file they want to examine for bad reads.

We can accomplish these goals by including the above command in a script that takes in user input
via a command line argument. We can slightly modify our `bad-reads-script.sh` file to do so. Use
`c` to copy your `bad-reads-script.sh` into a new script called `custom-bad-reads-script.sh`. Make
the following modifications to `custom-bad-reads-script.sh`:

```bash
filename=$1
grep -B1 -A2 -h NNNNNNNNNN $filename | grep -v '^--' > scripted_bad_reads.txt
```

`$1` is our command line argument. The line `filename=$1` tells Bash to take the first thing you type
after the name of the script itself and assign that value to a variable called filename.

For example, this script can be run in the following way to output the bad reads just from one file:

```bash
bash custom-bad-reads-script.sh SRR098026.fastq
```

We can then take a look at what the output file currently contains using `head scripted_bad_reads.txt`:

```output
@SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
NNNNNNNNNNNNNNNNCNNNNNNNNNNNNNNNNNN
+SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN
+SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.3 HWUSI-EAS1599_1:2:1:0:570 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN
```

This should be same output as using our original code and manually modifying the
original standalone code on the command line to "SRR098026.fastq" on the command line,
which should give us the same output as above:

```bash
$ grep -B1 -A2 -h NNNNNNNNNN SRR098026.fastq | grep -v '^--' > scripted_bad_reads.txt
head scripted_bad_reads.txt
```

```output
@SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
NNNNNNNNNNNNNNNNCNNNNNNNNNNNNNNNNNN
+SRR098026.1 HWUSI-EAS1599_1:2:1:0:968 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN
+SRR098026.2 HWUSI-EAS1599_1:2:1:0:312 length=35
!!!!!!!!!!!!!!!!#!!!!!!!!!!!!!!!!!!
@SRR098026.3 HWUSI-EAS1599_1:2:1:0:570 length=35
NNNNNNNNNNNNNNNNANNNNNNNNNNNNNNNNNN
```


