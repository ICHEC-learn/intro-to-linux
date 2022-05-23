---
title: "Working with files and directories"
teaching: 10
exercises: 0
questions:
- "How do I create, copy, delete files and directories?"
objectives:
- "How to create a directory hierarchy that matches a given diagram and how to navigate through it."
- "Delete, copy and move specified files and/or directories"
keypoints:
- "Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything,
  but is normally used to indicate the type of data in the file."
- "`cp [old] [new]` copies a file."
- "`mv [old] [path]` moves a file into the specified path, `mv [old] [new]` renames a file."
- "`mkdir [path]` creates a new directory."
- "`rmdir [path]` removes an empty directory. `rm [path]` removes a file. These are irreversible as the shell
  does not have a recycle bin."
---

## Creating and removing directories

Before we start with creating new directories and doing other operations, we should find a place to work, otherwise
material gets lost.

> ## Cloning a repository
>
> Online repositories contain written code in a directory. Github is a common place for people to uplaod their code in
> a safe place online, and so others can use it, comment and make changes. Many coding libraries are stored on GitHub,
> and it is where we store the materials for this lesson.
> 
> We are going to get you to clone this repo to your computer. Using the `cd` command, navigate to a directory which is
> easy for you to find (`Desktop`, or a `Courses` directory in `Documents`), and then type the following command in
> your terminal.
>
> `git clone https://github.com/ICHEC-learn/intro-to-linux.git`
>
> This will clone the repository, which includes slides for the lesson into the directory that you are in. It may take
> a minute. 
> 
> Then type `cd intro-to-linux/test` and you will arrive into that directory. Type `pwd` so you know where you are and
> `ls` to confirm that there is a single file called `README.md`.
>
{: .challenge}

`mkdir`

`rmdir`

## Removing files

`rm`

## Moving and Copying

`mv`

`cp`



<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

{% include links.md %}
