---
title: "Navigating through files and directories"
teaching: 10
exercises: 0
questions:
- "What is the directory tree?"
- "What is a path?"
- "What happens if I get lost?"
- "How do I move around?"
- "How can I see my files and folders?"
- "How can I use flags?"
objectives:
- "To gain understanding of the directory tree, and navigate through it as effectively as a GUI interface."
- "Explain the similarities and differences between files and directories."
- "Gain understanding of relative and actual paths."
- "Use options and arguments to change the behaviour of a shell command."
- "Demonstrate the usage of tab completion, and explain its advantages."
keypoints:
- "Information is stored in files, which are stored in directories. A directory is itself a file which contains 
  references to other files."
- "`..` means 'the directory above the current one' in the directory tree, whereas `.` on its own specifies 
  'the current directory'."
- "The `pwd` command will always show where you are at any time."
- "The `ls` command lists the contents of the present working directory. Additional options and arguments can filter 
  this list further."
- "The `cd` command allows you to navigate through directories, but you also need to direct it to where you want to go
  using `cd [path]`."
- "The root directory is specified by the root directory, referred to as `/`."
- "Directory names in a path are separated with `/` on Unix and Mac, but by `\\` on Windows."
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## The directory tree

If you are used to using click and select GUI operations for finding your way through files and folders on your
computer, then using the command line to navigate around for the first time is similar to being dropped into a 
thick maze in the dark without a torch. 

In Linux, everything is a file or a process, even directories. In Linux, folders are referred to as **directories**.
A directory is a file itself, one which contains references to other files. 

Each file has its own unique ID formed from the file name and a list of directories. This is why it is possible to have
different files with the same name in different directories, you have a unique identifier in the file system.

In the same way on Windows and Mac that you select folders and click to go deeper into the file system, Linux has this
method to by using what is known as the **directory tree**. You can see this in action on a Windows machine through the
top Search bar, and you can move around the directory tree using the forward and backwards arrow symbols. In Linux 
however, we need to physically tell the computer where we want to go.

This is what paths are used for. A path is essentially a route that traverses through a directory tree, which each
branch and "forks" in the tree separated by the `/` symbol. This symbol also denotes the **root** directory, the point
at which all directory trees start from. On Windows machines, in the Cmd prgoram, it is denoted with `\`. The root 
directory is usually restricted for administrative use. If you are on a desktop, you have access to this root 
directory. For supercomputers, this is restricted.

> ## Slashes
>
> Notice that there are two meanings for the `/` character.
> When it appears at the front of a file or directory name,
> it refers to the root directory. When it appears *inside* a path,
> it's just a separator.
{: .callout}

Let us look at a simple directory structure. This is an important concept to grasp as you move through a file system.

!!INSERT DIAGRAM!!

HOME - USERS - JOHN - DOCUMENTS - myfile

Each of the boxes refers to a directory, and the tree ends at `myfile`. You can see how the idea of a path arises, so
lets add some slashes in here to turn this directory structure into a path.

`/home/users/john/Documents/myfile`

This is what is known as an **absolute path**, which refers as the route from the root directory, to the file that we are
looking at, being `myfile`.

However, when we log into a machine, we are never put in the root directory. We are put in the home directory of whoever
is using the machine. John is logging on, so naturally he wants to be put where his material is. This is where we
introduce the term **relative path**, which is the path to a file or folder relative to where you are at any time. The
relative path in this case is;

`john/Documents/myfile`

We are in the directory `john`, and we wish to see the path to my file relative from where we are. Relative paths can
be more complex as we stay in one place and try and find a route to other places in our tree. But we will deal with
that later, let's look into our first few exercises.

> ## Locating yourself in a directory tree
>
> Given what you have learned so far, let's make things a bit trickier with a more complicated tree structure. Put into
> the chat the following;
> 
> 1. The absolute path to `text.txt`
> 2. The relative path to `text.txt` if you are in the `user1` directory.
> 
> > 
> > 1. `/home/users/user1/docs/text.txt`
> > 2. `./docs/text.txt`
> >
>
{: .challenge}



{% include links.md %}
