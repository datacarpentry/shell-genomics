---
layout: page
title: File manipulation
---

## File manipulation and more practice with pipes

Let's use the tools we've added to our tool kit so far, along with a few new ones, to example our SRA metadata file. First, let's navigate to the correct directory.

~~~
$ cd
$ cd shell_data/sra_metadata
~~~
{: .bash}

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

~~~
$ head -n 1 SraRunTable.txt
~~~
{: .bash}

~~~
BioSample_s	InsertSize_l	LibraryLayout_s	Library_Name_s	LoadDate_s	MBases_l	MBytes_l	ReleaseDate_s Run_s SRA_Sample_s Sample_Name_s Assay_Type_s AssemblyName_s BioProject_s Center_Name_s Consent_s Organism_Platform_s SRA_Study_s g1k_analysis_group_s g1k_pop_code_s source_s strain_s
~~~
{: .output}

That is only the first line of our file, but because there are a lot of columns, the output
likely wraps around your terminal window and appears as multiple lines. Once we figure out which
column our data is in, we can use a command called `cut` to extract the column of interest.

Because this is pretty hard to read, we can look at just a few column header names at a time by combining the `|` redirect and `cut`.

~~~
$ head -n 1 SraRunTable.txt | cut -f1-4
~~~
{: .bash}

`cut` takes a `-f` flag, which stands for "field". This flag accepts a list of field numbers,
in our case, column numbers. Here we are extracting the first four column names.

~~~
BioSample_s InsertSize_l      LibraryLayout_s	Library_Name_s    
~~~
{: .output}

The LibraryLayout_s column looks like it should have the information we want.  Let's look at some
of the data from that column. We can use `cut` to extract only the 3rd column from the file and
then use the `|` operator with `head` to look at just the first few lines of data in that column.

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
for just PAIRED and count the number of matches. For this, we will use the `|` operator twice
to combine `cut` (to extract the column we want), `grep` (to find matches) and `wc` (to count matches).

~~~
$ cut -f3 SraRunTable.txt | grep PAIRED | wc -l
~~~
{: .bash}

~~~
2
~~~
{: .output}

We can see from this that we have only two paired-end libraries in the samples we submitted for 
sequencing.

> ## Exercise
>
> How many single-end libraries are in our samples? 
>
>> ## Solution
>> ~~~
>> $ cut -f3 SraRunTable.txt | grep SINGLE | wc -l
>> ~~~
>> {: .bash}
>> 
>> ~~~
>> 35
>> ~~~
>> {: .output}
>>
> {: .solution}
{: .challenge}

#### How many of each class of library layout are there?  

We can extract even more information from our metadata table if we add in some new tools: `sort` and `uniq`. The `sort` command will sort the lines of a text file and the `uniq` command will
filter out repeated neighboring lines in a file. You might expect `uniq` to
extract all of the unique lines in a file. This isn't what it does, however, for reasons
involving computer memory and speed. If we want to extract all unique lines, we 
can do so by combining `uniq` with `sort`. We'll see how to do this soon.

For example, if we want to know how many samples of each library type are recorded in our table,
we can extract the third column (with `cut`), and pipe that output into `sort`. 

~~~
$ cut -f3 SraRunTable.txt | sort
~~~
{: .bash}

If you look closely, you might see that we have one line that reads "LibraryLayout_s". This is the 
header of our column. We can discard this information using the `-v` flag in `grep`, which means 
return all the lines that **do not** match the search pattern.

~~~
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort
~~~
{: .bash}

This command returns a sorted list (too long to show here) of PAIRED and SINGLE values. We can use
the `uniq` command to see a list of all the different categories that are present. If we do this,
we see that the only two types of libraries we have present are labelled PAIRED and SINGLE. There 
aren't any other types in our file.

~~~
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq
~~~
{: .bash}

~~~
PAIRED
SINGLE
~~~
{: .output}

If we want to count how many of each we have, we can use the `-c` (count) flag for `uniq`. 

~~~
$ cut -f3 SraRunTable.txt | grep -v LibraryLayout_s | sort | uniq -c
~~~
{: .bash}

~~~
2 PAIRED
35 SINGLE
~~~
{: .output}

> ## Exercise
>
> 1. How many different sample load dates are there?   
> 2. How many samples were loaded on each date?  
> 
>> ## Solution
>>  
>> 1. There are two different sample load dates.  
>>
>>    ~~~
>>    cut -f5 SraRunTable.txt | grep -v LoadDate_s | sort | uniq
>>    ~~~
>>    {: .bash}
>>
>>    ~~~
>>    25-Jul-12
>>    29-May-14
>>    ~~~
>>    {: .output}
>>
>> 2. Six samples were loaded on one date and 31 were loaded on the other.
>>
>>    ~~~
>>    cut -f5 SraRunTable.txt | grep -v LoadDate_s | sort | uniq -c
>>    ~~~
>>    {: .bash}
>>
>>    ~~~
>>     6 25-Jul-12
>>    31 29-May-14
>>    ~~~
>>    {: .output}
>>
> {: .solution}
{: .challenge}


#### Can we sort the file by library layout and save that sorted information to a new file?  

We might want to re-order our entire metadata table so that all of the paired-end samples appear
together and all of the single-end samples appear together. We can use the `-k` (key) flag for `sort` to
sort based on a particular column. This is similar to the `-f` flag for `cut`.

Let's sort based on the third column (`-k3`) and redirect our output to a new file.

~~~
$ sort -k3 SraRunTable.txt > SraRunTable_sorted_by_layout.txt
~~~
{: .bash}

#### Can we extract only paired-end records into a new file?  

We also might want to extract the information for all samples that meet a specific criterion 
(for example, are paired-end) and put those lines of our table in a new file. First, we need
to check to make sure that the pattern we're searching for ("PAIRED") only appears in the column
where we expect it to occur (column 3). We know from earlier that there are only two paired-end
samples in the file, so we can `grep` for "PAIRED" and see how many results we get.

~~~
$ grep PAIRED SraRunTable.txt | wc -l
~~~
{: .bash}

~~~
2
~~~
{: .output}

There are only two results, so we can use "PAIRED" as our search term to extract the paired-end 
samples to a new file.

~~~
$ grep PAIRED SraRunTable.txt > SraRunTable_only_paired_end.txt
~~~
{: .bash}

> ## Exercise
> Sort samples by load date and export each of those sets to a new file (one new file per
> unique load date). 
> 
> > ## Solution
> > 
> > ~~~ 
> > $ grep 25-Jul-12 SraRunTable.txt > SraRunTable_25-Jul-12.txt
> > $ grep 29-May-14 SraRunTable.txt > SraRunTable_29-May-14.txt
> > ~~~
> > {: .bash}
> >
> {: .solution}
{: .challenge}

