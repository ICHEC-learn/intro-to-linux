---
title: "Useful Tools"
teaching: 10
exercises: 0
questions:
- "How can I view file contents without needing a text editor"
- "How can I see the differences between two files?"
- "How can I zip files?"
- "What are `.tar` archives?"
- "How do wildcards work?"
- "How and why should I change permissions on a file?"
- "How can I search for a string in a file"
- "What are pipes and how do they work?"
- "What are sed and awk?"
objectives:
- "Use the `cat`, `less` and `more` commands to view file contents"
- "Write content to a file using `echo` and observe differences between files using `diff`"
- "Create and work with `.zip` files and `.tar` archives"
keypoints:
- "Point 1"
- "Point 2"
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## Viewing files contents

`echo`

`cat`

`more`

`less`

`head`

`tail`

## Spot the difference

`diff`

## Zipped files and archives

You may have encountered file type like `.zip`, `.gz` and `.tar` in your travels, and usually, operating systems such
as Windows might need specified programs to open them. Fortunately in Linux, you can create, zip, unzip, tar and un-tar
files like these.

Zip files are a single file containing one or more compressed files. Tar archives on the other hand are used to package
files together for backup or distribution purposes. They are sometimes called "tape archives". Many companies archive
data on tape for long-term storage, which requires less floor space and energy. These archives can then be zipped with
GNU Zip compression.

Zipping a file with GNU Zip compression is fairly straightforward, specify the file you want to zip.

~~~
touch new.txt
gzip new.txt
~~~
{: .language-bash}

On running this command, we get no confirmation that the file has been created, but we can use `ls` to confirm that our
new file `new.txt.gz` has been created. To unzip the file, we use `gunzip`

~~~
gunzip new.txt.gz
~~~
{: .language-bash}

This returns the file to its original state.

For `.tar` archives, we need to implement some flags to create it. To create an archive, we need the create `c` and 
file `f` flags, as well as specitfying a name for the tar archive.

~~~
tar -cf archive.tar new.txt
~~~
{: }

> ## `tar`-ing and `gzip`-ing a directory 
>
> Use `gzip`
> > ## Solution
> {: .solution}
{: .challenge}

## Wildcards

`* ? [] *?[]`

## File permissions

All files have owners. There is yourself, the machine user, a group owner, which is a group on a machine and then
others. 

Once you are on a machine and have multiple people on the same machine, it is important to know that others can access
your files. By default, you, the machine user and write and edit a file, but everyone else will have read-only 
privileges. Let's see what this looks like.

~~~
$ ls - lh hamlet.txt
~~~
{: .language-bash}

~~~
-rw-r--r--  1 user  staff  193K 11 Jan 12:00 hamlet.txt
~~~
{: .output}

The `-h` flag puts our output into human-readable format, so the size of our file is expressed in kilobytes. The main
area of interest for us though is on the left.

The first `-` may sometimes be filled with `d`, standing for directory, however our interest area are the 9 characters
to the right, which is divided into three sections, user, group and other

`chmod`


~~~
OWNER  GROUP  OTHER
r w x  r w x  r w x
1 1 1  0 0 0  0 0 0
  7      0      0
  |______|______|
         |
        700
~~~
{: .output}

> ## Who has what permissions?
> 
> Have a look at the different `rwx` permissions and numerical equivalents, and deduce who has what permissions, or who
> has been granted, or had permissions retracted
>
> 1. `rwxrwxr--`
> 2. `r--r--r--`
> 3. `755`
> 4. `740`
> 5. `rwxrw-r--`
> 6. `chmod u+x file`
> 7. `chmod go-wx file`
>
> > ## Solution
> >
> > 1. **User** and **group** can *read*, *write*, *execute*. **Other** can only *read* the file.
> > 2. **User**, **group** and **other** can only *read* the file
> > 3. **User** can *read*, *write* and *execute* the file. **Group** and **other** can *read* and *write* the file.
> > 4. **User** can *read*, *write* and *execute* the file, **Group** can *read* the file. **Other** cannot do anything.
> > 5. **User** can *read*, *write* and *execute* the file. **Group** can *read* and write the file. **Other** can read
> >    the file.
> > 6. The **user** has been given permission to *execute* the file.
> > 7. **Group** and **other** has has permissions to *read* and *write* the file retracted.
> {: .solution}
{: .challenge}

## Searching 

`grep` + pipes

## `sed` and `awk` sub-languages

We won't go into too much detail about these, as they are primarily used in bash scripting for advanced topics, but it
is still useful to know that such tools exist and that they can be used effectively.

### `sed` the UNIX stream editor

The `sed` command is another handy tool in UNIX that can be used for;
- Searching
- Finding and replacing
- Inserting/deleting

It is mainly used to edit files without the need to go into a file and change it directly. The format is as follows;

~~~
sed 'opt/act/flag' file
~~~
{: .language-bash}

### `awk` - a language within UNIX

The `awk` command accesses a sub-language within UNIX. In a similar way that Python can be accessed through the 
terminal, `awk` can be called within UNIX in a self-contained instance. It is a series of rules that take the form;

~~~
awk '(condition) {action}' file
~~~
{: .language-bash}

This can be used for anything from printing to complex mathematical statements, and can be useful in bash scripting
over multiple lines. We will cover bash scripting in more detail in [episode 6](06-bash-scripting.md).

{% include links.md %}
