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
> Online repositories contain written code in a directory. Github is a common place for people to upload their code in
> a safe place online, and so others can use it, comment and make changes. Many coding libraries are stored on GitHub,
> and it is where we store the materials for this lesson.
> 
> We are going to get you to clone this repo to your computer. Using the `cd` command, navigate to a directory which is
> easy for you to find (`Desktop`, or a `Courses` directory in `Documents`), and then type the following command in
> your terminal.
>
> ~~~
> git clone https://github.com/ICHEC-learn/intro-to-linux.git
> ~~~
> {: .language-bash}
>
> This will clone the repository, which includes slides for the lesson into the directory that you are in. It may take
> a minute. 
> 
> Then type `cd intro-to-linux/test` and you will arrive into that directory. Type `pwd` so you know where you are and
> `ls` to confirm that there is a single file called `README.md`.
>
{: .challenge}

Creating directories can be done very easily, with the `mkdir` command, followed by the name of the directory that you
wish to make. So, let us create a new directory and then us our `ls` command to show that is has been created 

~~~
$ mkdir mydir
$ ls -F
~~~
{: .language-bash}

~~~
README.md     mydir/
~~~
{: .output}

Now we will move into it, then confirm the directory that you are in.

~~~
$ cd mydir
$ pwd
~~~
{: .language-bash}

~~~
/Users/path/to/intro-to-linux/test/mydir/
~~~
{: .output}

Seems ok, doesn't it? Now let us move back up one directory and then remove our newly created directory with our new
command `rmdir` followed by the directory name.

~~~
$ cd ..
$ rmdir mydir
$ ls
~~~
{: .language-bash}

On typing `ls` you will notice that the directory `mydir` has been removed. So let's try this again with a challenge.

> ## Creating and removing a directory
>
> For this we are going to remove a directory that has a file in it, so.
> 1. Create a new directory
> 2. Change into the directory
> 3. Create a new file
> 4. Move back one directory
> 5. Remove it
>
> > ## Solution
> > 
> > 1. `mkdir newdir`
> > 2. `cd mydir`
> > 3. `touch myfile`
> > 4. `cd ..`
> > 5. `rmdir mydir`
> >
> > You may have noticed that we get an error message; `rmdir: newdir: Directory not empty` 
> >
> > We will now introduce the next command, which should be treated with care!
> {: .solution}
{: .challenge}

> ## Getting lost with `cd`
> 
> At the beginning, you may find that you get lost easily using `cd`, or more specifically, `cd ` on its own. There is
> a small shortcut that you can use, `cd -`, which puts you back to the previous directory you were in.
>
{: .callout}

## Removing files

That last challenge was designed to catch you out, as the `rmdir` command only works with directories that are empty.
We now introduce a command that should be handled with care. The `rm` command.

Why "handled with care" you may ask! Because the shell has no recycle bin that we can recover deleted files from 
(though most graphical interfaces to Unix do). Instead, when we delete files, they are unlinked from the file system so
that their storage space on disk can be recycled. Tools for finding and recovering deleted files do exist, but there's
no guarantee they'll work in any particular situation, since the computer may recycle the file's disk space right away.

So when you delete files and directories in the shell... it's gone! 

Let us try removing the `mydir` directory we created in the exercise.

~~~
$ rm mydir/
~~~
{: .language-bash}

~~~
rm: mydir: is a directory
~~~
{: .output}

So as you can see, we cannot use `rm` by itself to remove a directory, but let us move inside `mydir` and delete the
file from there

~~~
$ cd mydir/
$ rm myfile
$ ls
~~~
{: .language-bash}

The output here should be nothing, as we have deleted the file `myfile`. And remember, there is no way of getting it
back! Let's have a look at a way of using `rm` safely.

> ## Using `rm` safely
>
> By now you have seen the power of using `rm`, but we can add a useful flag, `-i` which will request the user to
> confirm we want the file removed. So, create a new file using `touch newfile`, and then try and remove it using the
> extra flag. 
>
> Notice a difference? What are the different options should you try?
> 
> > ## Solution
> > ~~~
> > $ touch newfile
> > $ rm -i newfile
> > ~~~
> > {: .language-bash}
> >
> > The `-i` option will prompt before (every) removal (use `Y` to confirm deletion or `N` to keep the file).
> >
> {: .solution}
{: .challenge}

You can use `rm` with multiple flags, but watch out as here be dragons! The `-r` flag can be particularly useful when 
trying to remove directories with a lot of files in it. Instead of removing each file one at a time, you can remove all
files in a directory and the directory itself by using;

~~~
$ rm -r mydir/
~~~
{: .language-bash}

As with other commands, unless the directory/files can be seen by the program in the current working directory, the 
command will not run.

Below you can find a few of the different flags that `rm` supports. 

| Flag | Action                                                                     |Danger Level|
|------|----------------------------------------------------------------------------|------------|
| `-i` | Requests confirmation before removing a file                               |    None    |
| `-r` | Removes the file hierarchy, removing the directory and all files within it |   Medium   |
| `-f` | Removes files without confirmation, regardless of file permissions         |    High    |

> ## Death command
> 
> You may have been able to deduce that there is a command that will remove everything with no prompting. Combined with
> wildcards, (which will be discussed in the next episode) this can remove **everything.**
> 
> ~~~
> $ rm -rf *
> ~~~
> {: .language-bash}
>
> So, a word of advice... don't ever type this!
{: .callout}

## Moving and Copying

`mv`

`cp`



<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

{% include links.md %}
