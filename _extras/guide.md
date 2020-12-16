---
layout: page
title: "Instructor Notes"
---

## Lesson motivation and learning objectives

Many researchers making the transition into genomics research (whether from another field or as their first research project) have
not had prior experience with command-line tools. They may quickly run into situations in which they need to use command-line tools
either because there is no good alternative for the type of anaysis they want to do or because they have so many data files that doing 
things manually on individual files is unfeasible. 

This lesson will introduce learners to fundamental skills needed for working with their computers through a command-line interface (using
the bash shell). They will learn how to navigate their file system, computationally manipulate their files (e.g. copying, moving, renaming), search files, redirect output and write shell scripts. By the end of the lesson, learners will be prepared to move on to using more advanced bioinformatic command line tools (see the lesson on [Data Wrangling and Processing](http://www.datacarpentry.org/wrangling-genomics/)).

## Lesson design

This lesson is meant to be taught in its entirety. For novice learners, schedule around 4 hours for this lesson. If your learners are 
already somewhat familiar with the bash shell, the earlier episodes can be condensed. 

This lesson uses data hosted on an Amazon Machine Instance (AMI). Instructors will be sent information on how to log-in to the AMI by the workshop coordinator a few days before the workshop. If you are running a self-organized workshop, register the workshop with our [self-organized workshop form](https://amy.carpentries.org/forms/workshop/) and send us an email at mailto:team@datacarpentry.org with information on how many people you expect to have at the workshop, and we'll start instances for you to use in the workshop. The day before the workshop, we'll send you the login information for your learners.

## Technical tips and tricks

#### Command Prompt Editing

Instructors might find it helpful to shorten their command prompt to allow better visibility of the commands they are typing, particularly if using the AMI.  This is because the prompt will contain additional information including the username and login for the instance, as well as filesystem location. This is especially useful when teaching the material online, as many learners may be splitting their screens and text wrapping may make the commands more difficult to identify if the prompt takes up a lot of space.

In order to edit your command prompt, type `PS1='$ '` into your shell and press enter. This will produce the simple "dollar space" prompt visible in the lesson content.  

In order to reset the command prompt, type `source .bashrc` in order to source the bash profile, or type `PS1="\u@\h:\w $ "` in order to set the prompt to show username, "@", hostname, ":", and current working directory (ie. the user's current location within the filesystem). 

NOTE: Editing the prompt is discussed in [lesson 01 - Introduction](https://datacarpentry.org/shell-genomics/01-introduction/index.html) under the 'Navigating your file system' section. This explains how to edit the prompt via `PS1='$ '` as here, so it would perhaps be best to *start* the lesson with the *default* prompt (as all the learners will and they can see that their screen will reassuringly match the instructor's screen at this point), and then instructors can choose to edit their prompt and talk through how they're doing that for learners' benefit at this section, or the instructor can just make the change early in the lesson for the visibility benefit, and explain to learners that they can find out how to do this in the lesson materials. 

Resetting the command prompt is not currently included in the lesson materials, so it might be useful to be familiar with this beforehand in case of learners' questions.

## Common problems

Learners will work through an Amazon Web Service (AWS) instance for this lesson. The workshop coordinator will set up AWS instances for 
your workshop a few days ahead of time. Put the links for all instances on your workshop Etherpad and have learners put their name next
to the instance they will use. This prevents learners from accidentally messing up another learner's filesystem.

The workshop coordinator usually sets up more AWS instances than needed for the registered learners. 
If a learner accidentally deletes or overwrites data files, you can have them change to a different AWS instance.


