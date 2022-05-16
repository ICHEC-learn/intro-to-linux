---
title: "Introducing Linux and the Command Line"
teaching: 10
exercises: 0
questions:
- "What is Linux and Unix?"
- "What is the command line and why is it used?"
- "How do I get help when using the command line?"
objectives:
- "Introduce the concept of Linux/UNIX operating systems"
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "UNIX is the original operating system, Linux refers to the kernel itself and is used by most top supercomputers."
- "On Linux systems, like supercomputers, everything is done on the command line."
- "Many commands need options (flags) beginning with a `-` to be utilised effecitvely"
- "Many commands need additional arguments to be passed into them to perform"
- "Whitespace matters. Every space makes a difference, so be careful what you are typing."
- "The `man` command will return usage and flags of any command you specify"
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## Background

Humans and computers commonly interact in many different ways, such as through a keyboard and mouse, touch screen
interfaces, or using speech recognition systems. The most widely used way to interact with personal computers is 
called a **graphical user interface** (GUI).

With a GUI, we give instructions by clicking a mouse and using menu-driven interactions.

While the visual aid of a GUI makes it intuitive to learn, this way of delivering instructions to a computer scales
very poorly. Take the following task as an example:

For a literature search, you have to copy the third line of one thousand text files in one thousand different 
directories and paste it into a single file. Using a GUI, you would not only be clicking at your desk for several
hours, but you could potentially also make an error in the process of completing this repetitive task. This is where
we take advantage of the Unix shell. The Unix shell is both a **command-line interface** (CLI) and a scripting
language, allowing such repetitive tasks to be done automatically and fast. If these tasks require a long time, having
then run in the background while you spent your time on more useful things can be a big advantage.

With the proper commands, the shell can repeat tasks with or without some modification as many times as we want.
Using the shell, the task in the literature example can be accomplished in seconds.

## Linux and UNIX

Most of us have either Windows or Mac operating systems (OS), and these are both GUI based, with Windows being by
far the most popular worldwide. Windows becomes more prone to malware as a result of this, whereas Mac, with its lower
user base, is less likely to be affected. Linux is even less affected by malware.

As a result, supercomputers will always have an OS with this type of setup. There are plenty of advantages of
doing so;
- 100% of TOP500 use it
- Operating system is more reliable and secure
- Open source software
- Massive toolsets for programming
- Very flexible and powerful

The most popular varietiy of Unix is GNU/Linux, which itself is a clone of Unix, with its source code available to
the general public.

Both Windows and Mac have their own command line interfaces like Linux, namely Command Prompt (Windows) and Terminal 
(Mac), with Terminal being much more effective. The OS is GUI based, with these extra applciations added on for 
developers. Linux however, is primarily command line based, with versions having GUI support (Ubuntu, Redhat, etc)

## The Shell

The shell is a program where users can type commands.
With the shell, it's possible to invoke complicated programs like climate modeling software or simple commands
that create an empty directory with only one line of code.

The most popular Unix shell is Bash (the Bourne Again SHell --- so-called because it's derived from a shell written
by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix and in most packages that provide Unix-like
tools for Windows.

Using the shell will take some effort and some time to learn.
While a GUI presents you with choices to select, CLI choices are not automatically presented to you, so you must
learn a few commands like new vocabulary in a language you're studying.

However, unlike a spoken language, a small number of "words" (i.e. commands) gets you a long way, and we'll cover
those essential few today.

The grammar of a shell allows you to combine existing tools into powerful pipelines and handle large volumes of data 
automatically. Sequences of commands can be written into a *script*, improving the reproducibility of workflows.

In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources
including high-performance computing systems.
As clusters and cloud computing systems become more popular for scientific data crunching,
being able to interact with the shell is becoming a necessary skill.
We can build on the command-line skills covered here
to tackle a wide range of scientific questions and computational challenges.

When the shell is first opened, you are presented with a **prompt**,
indicating that the shell is waiting for input.

~~~
$
~~~
{: .language-bash}

The shell typically uses `$ ` as the prompt, but may use a different symbol.
In the examples for this lesson, we'll show the prompt as `$ `.
Most importantly:
when typing commands, either from these lessons or from other sources,
*do not type the prompt*, only the commands that follow it.
Also note that after you type a command, you have to press the <kbd>Enter</kbd> key to execute it.

The prompt is followed by a **text cursor**, a character that indicates the position where your typing will appear. 
The cursor is usually a flashing or solid block, but it can also be an underscore or a pipe. 
You may have seen it in a text editor program, for example.

So let's try our first command, `ls` which is short for listing.
This command will list the contents of the current directory:

~~~
$ ls
~~~
{: .language-bash}

~~~
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
~~~
{: .output}

> ## Command not found
> If the shell can't find a program whose name is the command you typed, it
> will print an error message such as:
>
> ~~~
> $ ks
> ~~~
> {: .language-bash}
> ~~~
> ks: command not found
> ~~~
> {: .output}
>
> This might happen if the command was mis-typed or if the program corresponding to that command is not installed.
{: .callout}



> ## Anatomy of a command
> 
> Some commands need additional options to work, these can be in the form of flags (denoted as `-` for short options
> or `--` as long options), or arguments that are passed to the command
> 
>

The next few episodes will look more in detail on how to use commands to navigate around but first we need to briefly 
refer to the secure shell.

## SSH - Secure Shell

The command `ssh` known as secure shell follows an admin protocol that authenticates a remote user. To log into 
{{ site.remote.name }}, you will need to do so via `ssh`. You will need an ssh-key in which to do so. For more
information on ssh-keys, you can refer to the ICHEC [documentation](setting-up-ssh-keys) or check out our ichec-learn
repository on [intro-to-hpc](https://ichec-learn.github.io/intro-to-hpc/).

[setting-up-ssh-keys]: https://www.ichec.ie/academic/national-hpc/documentation/tutorials/setting-ssh-keys

{% include links.md %}
