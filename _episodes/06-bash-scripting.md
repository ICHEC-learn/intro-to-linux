---
title: "Bash Scripting"
teaching: 10
exercises: 0
questions:
- "What is bash scripting"
- "What are the different text editors?"
- "How can I run a bash script?"
objectives:
- "To use the vim or nano text editor to create a bash script"
- "Compile a simple code using a bash script"
keypoints:
- "Bash scripting and utilising text editors is the most important skill in Linux"
- "Without bash scripting, you are unable to submit jobs on an HPC, and the usability of Linux is limited."
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## Bash scripting

We are finally ready to see what makes the shell such a powerful programming environment. We are going to take the
commands we repeat frequently and save them in files so that we can re-run all those operations again later by typing
a single command. For historical reasons, a bunch of commands saved in a file is usually called a **bas script**,
but make no mistake, these are actually small programs.

## Text editors

There are plenty of text editors in bash scripting, but we will only focus on two here, `nano` and `vim`. Both have
their advantages and disadvantages.

Text editors work like commands, in the format `editor_name file_to_edit`, and opens up a window in which you can edit
the file. 

If the file that you are editing does not exist, then it creates one for you.

### `nano`

Nano is considered a very good option for beginners as it is simple to work with, and can help you edit anything, 
however if you wish to get things done quicker and have access to more features and shortcuts, then switch to `vim`.

### `vim`

Vim or **V**i **IM**proved is a highly flexible text editor designed for use on the command line and as its own GUI,
but is often the go-to and must know tool for anyone wishing to work on a UNIX system, mainly because all the tools for
editing text are there for you to use.

It can be tricky for beginners to get used to the different modes and shortcuts, but once gotten used to, it can save a
lot of time and effort.



> ## Getting used to text editors
>
> Using either `vim` or `nano`, get used to working with some of the commands to write text, open, close and save the
> files. 
>
> If you are using `vim` we recommend using this time to look at `vimtutor`. Type into your terminal
>
> ~~~
> vimtutor
> ~~~
> {: .language-bash}
>
> And you will get a window with an interactive tutorial with clear and instructive commands.
>
> ~~~
> ===============================================================================
> =    W e l c o m e   t o   t h e   V I M   T u t o r    -    Version 1.7      =
> ===============================================================================
> 
>      Vim is a very powerful editor that has many commands, too many to
>      explain in a tutor such as this.  This tutor is designed to describe
>      enough of the commands that you will be able to easily use Vim as
>      an all-purpose editor.
>     
>      ...       ...       ...       ...       ...       ...       ...       ...
>
>                         Lesson 1.1:  MOVING THE CURSOR
>
>
>   ** To move the cursor, press the h,j,k,l keys as indicated. **
>             ^
>             k              Hint:  The h key is at the left and moves left.
>       < h       l >               The l key is at the right and moves right.
>             j                     The j key looks like a down arrow.
>             v
>  1. Move the cursor around the screen until you are comfortable.
>
>      ...       ...       ...       ...       ...       ...       ...       ...
>
> ~~~
> {: .output}
{: .challenge}

## Creating a bash script

{% include links.md %}
