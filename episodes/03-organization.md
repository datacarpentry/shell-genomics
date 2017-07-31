---
title: "Project Organization"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---

# Getting your project started

Project organization is one of the most important parts of a sequencing project, but is often overlooked in the
excitement to get a first look at new data. While it's best to get yourself organized before you begin analysis,
it's never too late to start.  

You should approach your sequencing project in a very similar way to how you do a biological experiment, and 
ideally, begins with experimental design. We're going to assume that you've already designed a beautiful 
sequencing experiment to address your biological question, collected appropriate samples, and that you have 
enough statistical power. For all of those steps, collecting specimens, extracting DNA, prepping your samples,
you've likely kept a lab notebook that details how and why you did each step, but documentation doesn't stop at 
the sequencer!  

Every computational analysis you do is going to spawn many files, and inevitability, you'll 
want to run some of those analysis again. Genomics projects can quickly accumulates hundreds of files across 
tens of folders. Do you remember what PCR conditions you used to create your sequencing library? Probably not.
Similarly, you probably won't remember whether your best alignment results were in Analysis1, AnalysisRedone, 
or AnalysisRedone2; or which quality cutoff you used.  

Luckily, recording your computational experiments is even easier than recording lab data. Copy/Paste will become
your best friend, sensible file names will make your analysis traversable by you and your collaborators, and 
writing the methods section for your next paper will be a breeze. Let's look at the best practices for 
documenting your genomics project.   

Your future self will thank you.  


In this exercise we will setup a filesystem for the project we will be using over the next few days. We will 
also introduce you to some helpful shell commands, programs and tools, including: 
* ``mkdir``  
* ``history``  
* ``tail``  
* ``|``  
* ``nano``  
* ``>>``  

We will start by creating a directory that we can use for the rest of the workshop. First make sure you're in
your home directory, then type:  

    $ pwd

Hopefully you got the output: 

     /home/dcuser  

> ## Tip  
> When we give a command, rather than copying and pasting, type it into your shell window. Also, the `$`
indicates that we are at the command prompt, don't include that in your command.
{: .callout}

> ## Tip  
> If you aren't in your home directory, the easiest way to get there is to enter the command `cd`, which
> always returns you to home.  
{: .callout}

> ## Exercise  
> Try making the following directories using the `mkdir` command.  
> * dc_workshop   
> * dc_workshop/docs
> * dc_workshop/data  
> * dc_workshop/results  
{: .challenge}


Verify that you have created the directories:

    $ ls -R dc_workshop

If you have created these directories, you should get the following output:


    dc_workshop/:
    data  docs  results

    dc_workshop/data:

    dc_workshop/docs:

    dc_workshop/results: 

# Document your activity on the project

The `history` command is a convenient way to document all the commands you have used while analyzing and 
manipulating your project. Let's document the work we have done to create these folders. 

View the commands that you have used so far during this session using ``history``:


    $ history

The history likely contains many more commands that you have used just for these projects. Let's view the last
several commands so that focus on just what we need for the project.   

View the last n lines of your history (where n = approximately the last few lines you think relevant - for our example we will use the last 7:  

```bash    
$ history | tail -n 7
```

As you may remember from the shell lesson, the pipe `|` sends the output of history to the next program, in
this case `tail`. We have used the `-n` option to give the last 7 lines.  

Using your knowledge of the shell use the append redirect `>>` to create a file called
**dc_workshop_log_XXXX_XX_XX.txt** (Use the four-digit year, two-digit month, and two digit day, e.g.
dc_workshop_log_2015_07_30.txt)  

You may have noticed that your history may contain the `history` command itself. To remove this redundancy
from our log, lets use the `nano` text editor to fix the file:  

```bash
    $ nano dc_workshop_log
```

From the nano screen, you should be able to use your cursor to navigate, type, and delete any redundant lines.   

Add a dateline and comment to the line where you have created the directory, for example:   

```bash
# 2015_07_30   
# Created sample directories for the Data Carpentry workshop  
```

Next, remove any lines of the history that are not relevant by navigating to those lines and using your 
delete key.   

Close nano by hitting 'Control' and the 'X' key at the same time; notice in nano this is abbreviated '\^X'.
Nano will ask if you want to save. Type 'Y' for yes. When prompted for the 'File Name to Write', hit 'Enter'
to keep the same name and save.   

Now that you have created the file, move the file to 'dc_workshop/docs' using the `mv` command.  


> ## Questions  
> 1. What is the default number of lines that tail displays?  
> 2. What is the difference between `>` and `>>`?
{: .challenge}

## References
[A Quick Guide to Organizing Computational Biology Projects](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424)



