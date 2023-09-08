---
title: Etherpad template
subtitle: Template text to paste in to collaborative document
---

# Introduction to the Command Line for Genomic

**Date**

**Instructor**

**Helper**

**Website**
[https://datacarpentry.org/shell-genomics/instructor/index.html](https://datacarpentry.org/shell-genomics/instructor/index.html)

## Timings - EDIT FOR YOUR WORKSHOP


- Introducing the Shell 09:30-10:00 (30 mins)
- Navigating Files and Directories 10:00-10:50 (50 mins)
- Break 10:50-11:05 (15 mins)
- Working with Files and Directories 11:05-11:50 (45 mins)
- Redirection 11:50-12:35 (45 mins)
- Break 12:35-13:30 (55 mins)
- Writing Scripts and Working with Data 13:30-14:10 (40 mins)
- Project Organization 14:10-14:40 (30 mins)
- Wrap up and feedback 14:40-14:55 (15 mins)

## Attendees

Please write your name below to confirm attendance, and one thing you're hoping to get out of this workshop:

1. 2. 3. 4. 5. 
## Feedback

Link to feedback form if needed

## [Introducing the Shell](https://datacarpentry.org/shell-genomics/01-introduction.html)

### Exercise:

Use the `-l` option for the `ls` command to display more information for each item in the directory. 

What is one piece of additional information this long format gives you that you don’t see with the bare `ls` command?
- - -

## [Navigating Files and Directories](https://datacarpentry.org/shell-genomics/02-the-filesystem.html)

### Exercise: FINDING HIDDEN DIRECTORIES

First navigate to the `shell_data` directory. 
There is a hidden directory within this directory. Explore the options for `ls` to find out how to see hidden directories. 
List the contents of the directory and identify the name of the text file in that directory.

**Hint:** hidden files and folders in Unix start with ., for example .my_hidden_directory


### Exercise: NAVIGATING PRACTICE

Navigate to your home directory. From there, list the contents of the `untrimmed_fastq` directory.

### Exercise: RELATIVE PATH RESOLUTION

Using the filesystem diagram on the lesson page [below](https://datacarpentry.org/shell-genomics/02-the-filesystem.html), if pwd `displays` `/Users/thing`, what will ls .`./backup display`?

Put a `+` next to the answer you think is correct.

1. ../backup: No such file or directory
2. 2012-12-01 2013-01-08 2013-01-27
3. 2012-12-01/ 2013-01-08/ 2013-01-27/
4. original pnas_final pnas_sub


## [Working with Files and Directories](https://datacarpentry.org/shell-genomics/03-working-with-files.html)

### Exercise: 

Do each of the following tasks from your current directory using a single `ls` command for each:

1.  List all of the files in `/usr/bin` that start with the letter ‘c’.
2.  List all of the files in `/usr/bin` that contain the letter ‘a’.
3.  List all of the files in `/usr/bin` that end with the letter ‘o’.

Bonus: List all of the files in `/usr/bin` that contain the letter ‘a’ or the letter ‘c’.

**Hint:** The bonus question requires a Unix wildcard that we haven’t talked about yet. Try searching the internet for information about Unix wildcards to find what you need to solve the bonus problem.
- - -
### Exercise: echo and wildcards

`echo` is a built-in shell command that writes its arguments, like a line of text to standard output. 
The `echo` command can also be used with pattern matching characters, such as wildcard characters. 
Here we will use the `echo` command to see how the wildcard character is interpreted by the shell.

```bash
$ echo *.fastq
```
What would the output look like if the wildcard could not be matched?

Compare the outputs of 

1. `echo *.missing` 
2. `ls *.missing`
- - -
### Exercise: command history

Find the line number in your `history` for the command that listed all the `.sh` files in `/usr/bin`. 
Rerun that command.

- - -

### Exercise: Examining Files

1. Print out the contents of the `~/shell_data/untrimmed_fastq/SRR097977.fastq` file. What is the last line of the file?

2. From your home directory, and without changing directories, use one short command to print the contents of all of the files in the
`~/shell_data/untrimmed_fastq` directory.

- - -

### Exercise: Examining Files

Use `less` on the file SRR097977.fastq and find the next three nucleotides (characters) after the first instance of the sequence `TTTTT`?

- - -

### Exercise: 

Starting in the `shell_data/untrimmed_fastq/` directory, do the following:

1. Make sure that you have deleted your backup directory and all files it contains.
2. Create a backup of each of your FASTQ files using cp. (Note: You’ll need to do this individually for each of the two FASTQ files. We haven’t learned yet how to do this with a wildcard.)
3. Use a wildcard to move all of your backup files to a new backup directory.
4. Change the permissions on all of your backup files to be write-protected.

- - -

## [Redirection](https://datacarpentry.org/shell-genomics/04-redirection.html)

### EXERCISE:

1. Search for the sequence `GNATNACCACTTCC in the `SRR098026.fastq` file. Have your search return all matching lines and the name (or identifier) for each sequence that contains a match.

2. Search for the sequence `AAGTT` in both FASTQ files. Have your search return all matching lines and the name (or identifier) for each sequence that contains a match.
- - -

### EXERCISE

How many sequences are there in `SRR098026.fastq`? Remember that every sequence is formed by four lines.

- - -

### EXERCISE

How many sequences in `SRR098026.fastq` contain at least 3 consecutive Ns?

- - -

### EXERCISE

Print the file prefix of all of the `.txt` files in our current directory.

- - -

### EXERCISE

Remove `_2019` from all of the `.txt` files.

- - - 

## [Writing Scripts and Working with Data](https://datacarpentry.org/shell-genomics/05-writing-scripts.html)

### EXERCISE

Open `README.txt` and add the date to the top of the file and save the file.

- - -

### EXERCISE

We want the script to tell us when it’s done.

Open `bad-reads-script.sh` and add the line echo `"Script finished!"` after the grep command and save the file.
Run the updated script.

- - -

## [Project Organization[(https://datacarpentry.org/shell-genomics/06-organization.html)

### EXERCISE
Use the `mkdir` command to make the following directories:

```
dc_workshop
dc_workshop/docs
dc_workshop/data
dc_workshop/results
```
- - -

### EXERCISE

Using your knowledge of the shell, use the append redirect >> to create a file called `dc_workshop_log_XXXX_XX_XX.sh` (Use the four-digit year, two-digit month, and two digit day, e.g. `dc_workshop_log_2017_10_27.sh`)

## Evaluation and Feedback

Instructors and lesson maintainers use these responses to improve the lesson.
It's very helpful!

#### Please list one thing you liked or found particularly useful

- - - - - 
#### Please list another thing you found less useful, or that could be improved

- - - - - 
