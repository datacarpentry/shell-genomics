---
title: "Writing Scripts"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- Navigate the Unix file system.
- Copy and move files.
- Use the history command to review recent commands in the shell.
- Use the nano text editor to modify text files.
- Use arguments to modify the behavior of command line commands.
keypoints:
- "First key point."
---

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

![nano1.png](../img/nano1.png)

Type in your command, so it looks like

![nano2.png](../img/nano2.png)

Now we want to save the file and exit. At the bottom of nano, you see the "^X Exit". That
means that we use Ctrl-X to exit. Type `Ctrl-X`. It will ask if you want to save it. Type `y` for yes.
Then it asks if you want that file name. Hit 'Enter'.

Now you've written a file. You can take a look at it with less or cat, or open it up again and edit it.

***
**Exercise**

Open 'awesome.sh' and add "echo AWESOME!" after the grep command and save the file.

We're going to come back and use this file in just a bit.

***


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
