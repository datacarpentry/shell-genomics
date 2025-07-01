---
title:  Searching Files and Redirecting
teaching: 15
exercises: 5
---

::: objectives
-   Employ the `grep` command to search for information within files.
-   Redirect the results of a command to a file.
-   Construct command pipelines with two or more stages using the pipe operator.
:::

::: questions
-   How can I search for specific content within files?
-   How can I save my command output to a file?
-   How can I combine existing commands to do new things?
:::

## Searching files with `grep`

In a previous episode, we learned how to search within a file using `less`. We can also search within files without opening them by using the `grep` command. `grep` is a command-line utility for searching plain-text files for lines that match a specific string of characters or a particular pattern. For this lesson, we will focus on searching for strings.

Let's search for strings inside our metadata file `SraRunTable.txt`. First, make sure you are in the correct directory:

::: callout
## SraRunTable

SraRunTable.txt is a tab-delimited text metadata file downloaded from the NCBI Sequence Read Archive (SRA). It contains crucial information about a set of sequencing "runs" (individual sequencing experiments) associated with a particular SRA project or experiment.

Essential Identifiers:

-   **Run** (or Run_s or Run_ID): This is the most crucial header. It contains the SRR accession number (e.g., SRR097977), which is the unique identifier for a specific sequencing run. You'll use this to download the actual FASTQ or SRA files.
-   **BioSample** (or BioSample_s or BioSample_ID): The SAMN accession number (e.g., [SAMN00205533](https://www.ebi.ac.uk/ena/browser/view/SAMN00205533?dataType=BIOSAMPLE)) refers to the ENA BioSample record, which provides a more detailed description of the biological source material.
-   **Sample** (or SRA_Sample_s or Sample_ID): The SRS accession number (e.g., SRS167141) identifies the biological sample from which the sequencing data was derived. Multiple experiments and runs might originate from the same sample.

Information on how to download the SraRunTable.txt can be found in the lesson [Examining Data on the NCBI SRA Database](https://datacarpentry.github.io/organization-genomics/03-ncbi-sra.html).
:::

```bash
$ cd ~/shell_data/sra_metadata
```

You can use `less` to quickly inspect the contents of `SraRunTable.txt`:

```bash
$ less SraRunTable.txt
```

```output
BioSample_s     InsertSize_l    LibraryLayout_s Library_Name_s  LoadDate_s      MBases_l        MBytes_l        ReleaseDate_s   Run_s   SRA_Sample_s    Sample_Name_s   Assay_Type_s    AssemblyName_s  BioProject_s    Center_Name_s   Consent_s       Organism_s      Platform_s      SRA_Study_s     g1k_analysis_group_s    g1k_pop_code_s  source_s        strain_s
SAMN00205533    0       SINGLE  CZB152  29-May-14       149     100     25-Mar-11       SRR097977       SRS167141       CZB152  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205558    0       SINGLE  CZB154  29-May-14       627     444     25-Mar-11       SRR098026       SRS167166       CZB154  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205559    0       SINGLE  CZB199  29-May-14       157     118     25-Mar-11       SRR098027       SRS167167       CZB199  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205560    0       SINGLE  REL1166A        29-May-14       627     440     25-Mar-11       SRR098028       SRS167168       REL1166A        WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205561    0       SINGLE  REL10979        29-May-14       140     94      25-Mar-11       SRR098029       SRS167169       REL10979        WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
..SraRunTable.txt
```

### Searching for exact and partial matches

Let's find information about one of our samples using its SRR accession number, `SRR097977`.

```bash
$ grep SRR097977 SraRunTable.txt
```

This command prints any line in the file that contains the string `SRR097977`.

```output
SAMN00205533    0       SINGLE  CZB152  29-May-14       149     100     25-Mar-11       SRR097977       SRS167141     CZB152  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA      SRP004752       <not provided>  <not provided>  <not pro
```

`grep` can also match parts of a larger string. For example, we can search for `ZDB172`:

```bash
$ grep ZDB172 SraRunTable.txt
```

The output includes lines containing `ZDB172-SE` and `ZDB172-PE` because they both contain the string `ZDB172`.

```output
SAMN00205573    0       SINGLE  ZDB172-SE       29-May-14       59      48      25-Mar-11       SRR098042       SRS167181       ZDB172  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205573    2729    PAIRED  ZDB172-PE       29-May-14       1620    635     25-Mar-11       SRR098043       SRS167181       ZDB172  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
```

If you want to match `ZDB16-SE` use this exact word

```bash
$ grep  ZDB172-SE SraRunTable.txt
```

```output
SAMN00205573    0       SINGLE  ZDB172-SE       29-May-14       59      48      25-Mar-11       SRR098042       SRS167181       ZDB172  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
```

In some cases the word you want to match `ZDB16` in a file is contained within the text of another word e.g. `ZDB165`

```bash
$ grep ZDB16 SraRunTable.txt
```

```output
SAMN00205563    0       SINGLE  ZDB16   29-May-14       606     424     25-Mar-11       SRR098031       SRS167171       ZDB16   WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN01095547    0       SINGLE  ZDB165  25-Jul-12       155     106     26-Jul-12       SRR527254       SRS351861       ZDB165  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
```

To match an exact word, you can use the -w flag (for "word").

```bash
$ grep -w ZDB16 SraRunTable.txt
```

```output
SAMN00205563    0       SINGLE  ZDB16   29-May-14       606     424     25-Mar-11       SRR098031       SRS167171       ZDB16   WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA        SRP004752       <not provided>  <not provided>  <not provided>  REL606
```


### Case-insensitive matching

By default, `grep` is case-sensitive. This means that `SINGLE` is different from `single`. Let's see:

```bash
$ grep SINGLE SraRunTable.txt
```

Now, try searching for Single:

```bash
$ grep Single SraRunTable.txt
```

```output
# (No output, because "Single" doesn't appear with a capital 'S' in the file)
```

To perform a case-insensitive search, use the -i flag (for "ignore-case"):

```bash
$ grep -i Single SraRunTable.txt
```

```output
SAMN00205533	0	SINGLE	CZB152	29-May-14	149	100	25-Mar-11	SRR097977	SRS167141	CZB152	WGS	<not provided>	PRJNA188723	MSU	public	Escherichia coli B str. REL606	ILLUMINA	SRP004752	<not provided>	<not provided>	<not provided>	REL606
SAMN00205558	0	SINGLE	CZB154	29-May-14	627	444	25-Mar-11	SRR098026	SRS167166	CZB154	WGS	<not provided>	PRJNA188723	MSU	public	Escherichia coli B str. REL606	ILLUMINA	SRP004752	<not provided>	<not provided>	<not provided>	REL606
... (same output as `grep SINGLE`, as it now matches regardless of case)
```

### Counting matches

Sometimes, you don't need to see the matching lines, but just want to know how many there are. The `-c` flag (for "count") tells `grep` to output only the number of matching lines.

```bash
$ grep -c SINGLE SraRunTable.txt
```

```output
35
```


### Inverting matches

You can also find lines that **do not** match a pattern by using the `-v` flag (for "invert"). For example, we can find all records that are not `PAIRED` reads.

```bash
$ grep -v PAIRED SraRunTable.txt
```

This command will print the header line (which does not contain the word `PAIRED`) and all lines for `SINGLE` reads.

```output
BioSample_s     InsertSize_l    LibraryLayout_s Library_Name_s  LoadDate_s      MBases_l        MBytes_l        ReleaseDate_s   Run_s   SRA_Sample_s    Sample_Name_s   Assay_Type_s    AssemblyName_s    BioProject_s    Center_Name_s   Consent_s       Organism_s      Platform_s      SRA_Study_s     g1k_analysis_group_s    g1k_pop_code_s  source_s        strain_s
SAMN00205533    0       SINGLE  CZB152  29-May-14       149     100     25-Mar-11       SRR097977       SRS167141     CZB152  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA      SRP004752       <not provided>  <not provided>  <not provided>  REL606
SAMN00205534    0       SINGLE  CZB153  29-May-14       149     100     25-Mar-11       SRR097978       SRS167142       CZB153  WGS     <not provided>  PRJNA188723     MSU     public  Escherichia coli B str. REL606  ILLUMINA      SRP004752       <not provided>  <not provided>  <not provided>  REL606
...
```

:::::::::::::::::::::::::::::::::::::::  challenge
## Exercise

Let's search for the string `PAIRED` in the `SraRunTable.txt` file.

:::::::::::::::  solution
## Solution

```bash
$ grep PAIRED SraRunTable.txt
```

This command returns a lot of output to the terminal. Every single line in the `SraRunTable.txt` file that contains "PAIRED" is printed to the terminal.
:::::::::::::::  
:::::::::::::::::::::::::::::::::::::::  

## Redirecting Output

`grep` is useful for finding matching lines, but often we want to save those results to work with them further. We can do this with **output redirection**. Instead of printing to the terminal, we can redirect the output to a file.

The `>` operator redirects output to a file, creating the file if it doesn't exist and **overwriting** it if it does.

Let's save  the `SRR097977` read record to a new file called `metadata.txt`.

```bash
$ grep SRR097977 SraRunTable.txt > metadata.txt
```

The command produces no output to the terminal, but if you type `ls`, you will see the new file. We can check its contents with `wc -l`, which counts the number of lines in a file.

```bash
$ wc -l metadata.txt
```

```output
1
```

Be careful: using `>` will overwrite the destination file. For example:

```bash
$ grep SRR098026 SraRunTable.txt > metadata.txt
$ wc -l metadata.txt
1 metadata.txt

$ grep SRR097977 SraRunTable.txt > metadata.txt
$ wc -l metadata.txt
1 metadata.txt
```
The second command overwrote the results of the first. To **append** to a file instead of overwriting it, use the `>>` operator.

```bash
$ grep SRR098026 SraRunTable.txt > metadata.txt
$ grep SRR097977 SraRunTable.txt >> metadata.txt
$ wc -l metadata.txt
2 metadata.txt
```
Now, the file contains the results from both commands.

## Constructing Command Pipelines

Redirection is useful for saving command output, but what if we only need to process data on-the-fly without creating intermediate files? We can combine commands using a **pipeline**. The `|` operator (called the "pipe") takes the standard output of the command on its left and uses it as the standard input for the command on its right. This allows us to chain multiple commands together to perform complex tasks efficiently.

For example, instead of saving the `grep` results to a file and then running `head` on it, we can do it in one step:

```bash
$ grep PAIRED SraRunTable.txt | head
```

This is a very common and powerful pattern. It lets you chain multiple commands together to perform complex tasks without creating temporary files. This is especially useful when dealing with large files, like `SraRunTable.txt`, where creating many intermediate files can consume significant disk space and time.

### Combining `grep` with `cut`

Another powerful command to use in pipelines is `cut`. The `cut` command extracts selected portions of each line from a file or standard input. It's particularly useful for working with tabular data, where you might want to select specific columns.

The `SraRunTable.txt` file is tab-delimited, meaning its columns are separated by tab characters. We can use `cut` with the `-f` option to specify which fields (columns) to extract. For example, to extract the 1st, 9th, 10th, 11th, 14th, and 19th columns (which correspond to `BioSample_s`, `Run_s`, `SRA_Sample_s`, `Sample_Name_s`, `BioProject_s`, and `SRA_Study_s` respectively), we would use:

```bash
$ cut -f1,9-11,14,19 SraRunTable.txt
```

```output
BioSample_s	Run_s	SRA_Sample_s	Sample_Name_s	BioProject_s	SRA_Study_s
SAMN00205533	SRR097977	SRS167141	CZB152	PRJNA188723	SRP004752
SAMN00205558	SRR098026	SRS167166	CZB154	PRJNA188723	SRP004752
...
```

Now, let's combine `grep` and `cut` using a pipe. Suppose we want to find all records for `SRR097977` and then extract only the `BioSample_s`, `Run_s`, `SRA_Sample_s`, `Sample_Name_s`, `BioProject_s`, and `SRA_Study_s` columns. We can do this in a single pipeline:

```bash
$ grep SRR097977 SraRunTable.txt | cut -f1,9-11,14,19
```

```output
SAMN00205533	SRR097977	SRS167141	CZB152	PRJNA188723	SRP004752
```

This pipeline first filters the `SraRunTable.txt` file for lines containing `SRR097977` using `grep`, and then `cut` processes only those filtered lines, extracting the specified columns. This approach is highly efficient because `cut` doesn't need to read the entire `SraRunTable.txt` file; it only processes the data passed to it by `grep`. This saves time and resources, especially with very large datasets common in genomics.

:::::::::::::::::::::::::::::::::::::::  challenge
## Exercise

Using a pipe `|`, select `PAIRED` reads sample present in the `SraRunTable.txt` file and then extract only the `Run_s` (column 9) and `LibraryLayout_s` (column 3) for those reads.

:::::::::::::::  solution
## Solution

```bash
$ grep PAIRED SraRunTable.txt | cut -f9,3
```
```output
PAIRED	SRR098033
PAIRED	SRR098043
```


This command first filters for `SINGLE` reads and passes the output using a pipe `|` to `cut` which then extracts the specified columns.
:::::::::::::::
:::::::::::::::::::::::::::::::::::::::  

## Summary of `grep` Options

Here's a summary of the `grep` options covered in this lesson:

| Option | Description                                     | Example Usage                     |
| :----- | :---------------------------------------------- | :-------------------------------- |
| (none) | Search for lines containing a specified string. | `grep PAIRED SraRunTable.txt`     |
| `-c`   | Count the number of matching lines.             | `grep -c SINGLE SraRunTable.txt`  |
| `-v`   | Invert the match; show lines that *do not* match. | `grep -v PAIRED SraRunTable.txt`  |
| `-w`   | Match only whole words.                         | `grep -w ZDB16 SraRunTable.txt`   |
| `-i`   | Perform a case-insensitive search.              | `grep -i single SraRunTable.txt`  |

:::::::::::::::::::::::::::::::::::::::: keypoints
- `grep` is a powerful search tool with many flags/options for customization.
- `>` redirects output to a file, overwriting its previous content.
- `>>` appends output to a file, preserving its existing content.
- `|` creates a pipeline, sending the output of one command as input to another.
:::::::::::::::::::::::::::::::::::::::: 
