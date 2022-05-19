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

> ## Starting a terminal
>
> Mac and Linux users have life easy, the Terminal application has all the UNIX commands you will ever need. Windows
> users do not have things as easy, as the Command Prompt app does not support any UNIX commands.
>
> There are two commonly used Linux terminal emulators, MobaXterm and Git Bash.
>
> If you have already installed [MobaXterm (Portable Edition)](https://mobaxterm.mobatek.net/download-home-edition.html)
> and are used to the setup, feel free to continue using it.
>
> If you do not yet have a terminal emulator, or find MobaXterm confusing, then we recommend you to install 
> [Git Bash](https://git-scm.com/download/win).
>
> Take a minute to set install or start your terminal emulator. It can continue in the background as we continue
>
{: .challenge}

## The Shell

The shell is a program where users can type commands, and is accessed through a terminal. With the shell, it's possible
to invoke complicated programs like climate modeling software or simple commands that create an empty directory with
only one line of code.

The most popular Unix shell is Bash (the Bourne Again SHell --- so-called because it's derived from a shell written by 
Stephen Bourne). Bash is the default shell on most modern implementations of Unix and in most packages that provide 
Unix-like tools for Windows (MobaXterm, Git Bash, PuTTy).

Using the shell will take some effort and some time to learn.
While a GUI presents you with choices to select, CLI choices are not automatically presented to you, so you must
learn a few commands like new vocabulary in a language you're studying.

However, unlike a spoken language, a small number of "words" (i.e. commands) gets you a long way, and we'll cover
those essential few today.

## The command line

The grammar of a shell allows you to combine existing tools into powerful pipelines and handle large volumes of data 
automatically. Sequences of commands can be written into a *script*, improving the reproducibility of workflows.

In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources including 
high-performance computing systems. As clusters and cloud computing systems become more popular for scientific data
crunching, being able to interact with the shell is becoming a necessary skill. We can build on the command-line skills
covered here to tackle a wide range of scientific questions and computational challenges.

When the shell is first opened, you are presented with a **prompt**, indicating that the shell is waiting for input. 
This can depend on the type of shell, but is typically `$` or `%`.

Most importantly, when typing commands, either from these lessons or from other sources,
*do not type the prompt*, only the commands that follow it.
Also note that after you type a command, you have to press the `Enter` key to execute it.

If the command has executed, depending on the command, no output will appear on the screen and you will be returned to
the prompt. This is an indication that your command has executed as specified.

The prompt is followed by a **text cursor**, a character that indicates the position where your typing will appear. 
The cursor is usually a flashing or solid block, but it can also be an underscore (`_`) or a pipe (`|`). You may have
seen it in a text editor program, for example.

The shell then requires information on what it needs to work on, in the same way a mouse won't click unless you tell it
or a keyboard won't type out words. The command line needs input to work. These inputs are called *commands*. 
A very simple command can be as shown below.

~~~
courseXX@login2:~$ ls
~~~
{: .input}

All the information to the left of the `$` is the prompt, and we are entering the command `ls`, which is short for
list. It lists out the contents of the directory that you are in. For Windows and Mac, this is shown automatically, as
you move from folder to folder. In Linux you need to specify it.

Most commands have additional options to make them more specific, and these are known as **flags**. Flags are accessed
by using `-` for a single letter flag or `--` for longer options. Below is an example of a command with both short and
long option flags

~~~
courseXX@login2:~$ ls -l --all
~~~
{: .input}

Here, the `-l` gives a full list of the properties of a directory that you are in, and the `--all` shows hidden files. 
Hidden files themselves are important, and we will come back to them later.

Some commands however cannot work by themselves and flags alone. What if you wanted to copy a file from one place to
another? Additional arguments are needed. With our `ls` command, we can also introduce an argument as well as all the
flags

~~~
courseXX@login2:~$ ls -l --all test/
~~~
{: .input}

Here the argument we are passing is `test/`, which is a directory

Many commands come with additional flags


An important thing to remember is that you will make mistakes, and that computers are not human, so if a command is not
exactly correct it will raise an error.

> ## Command not found
>
> If the shell can't find a program whose name is the command you typed, it will print an error message such as:
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

> ## Order matters!
> 
> Typing a command, arguments or flags out of order can result in mistakes and errors being raised by the shell. Have a
> look at the code below, and try and deduce which one(s) are in the correct order, and which ones will not work.
>
> 1. `la -s`
> 2. `ls --a`
> 3. `ls -`
> 4. `ls -z`
> 5. `-l ls`
> 6. `ls -all --l prog/`
> 7. `ls --all -l prog/`
> 8. `ls -l all`
> 9. `prog/ ls`
> 10. `ls -l --all prog/`
> > 
> > ## Solution
> >
> > 1. No, `la` doesn't exist despite `-s` being a valid flag.
> > 2. No, `--a` is a short flag option.
> > 3. No, there is no option specified.
> > 4. No, `-z` is an invalid flag.
> > 5. No, the command must come before the flag.
> > 6. No, `-all` should be `--all` and `--l` should be `-l`.
> > 7. Yes, the order of the flags doesn't matter.
> > 8. Technically yes, but only if there is an item called all. We are missing the `--` if we want to use it as a 
> >    flag.
> > 9. No, the command comes before the argument.
> > 10. Yes, this vertically lists all the files (+ hidden ones) in `prog/`.
> {: .solution}
{: .challenge}

You may have made a few mistakes there, if not, then well done, if so, that's also ok! Programmers make Linux typos and
errors on a minutely basis, never mind hourly! Its often worth pointing out that some flags and options may work on
Linux itself but not Mac or Windows terminal emulators. The shell program can vary, but for the most part stays fairly
consistent.

It is often the case that you make a typo at the beginning of a long command, and you may feel like you need to retype
the whole thing. No need, as there are a few keyboard shortcuts that you may find helpful.

| Action                    | Keyboard     | Action                    | Keyboard         |
|---------------------------|--------------|---------------------------|------------------|
| Move left                 | `left arrow` | Delete previous character | `Backspace`      |
| Move right                | `right arrow`| Delete previous word      | `Ctrl w`         |
| Move to beginning of line | `Ctrl a`     | Delete next character     | `Ctrl d`/`Delete`|
| Move to end of line       | `Ctrl e`     | Delete rest of the line   | `Ctrl k`         |
| Previous command entered  | `up arrow`   | Next command entered      | `down arrow`     |

In the next few episodes we will learn about the different commands, and get practice on using them.

{% include links.md %}
