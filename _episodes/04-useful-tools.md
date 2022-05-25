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

To view file contents, we need to first introduce a small command often used in bash scripting to post messages. It is
effectively the `print` or `stdout` of UNIX, with a catchy name, `echo`

Let's see how it works.

~~~
$ echo "this message"
~~~
{: .language-bash}

~~~
this message
~~~
{: .output}

Seems fairly useless here, but can be a very good way to debug a bash script, to find where the program fails. Now
let's introduce the `>` sign, which here will put the message we want into a file. We'll do this a couple of times as
it will lead into the next section.

~~~
$ echo "This message is correct" > correct.txt
$ echo "This message is incorrect" > incorrect.txt
~~~
{: .language-bash}

> ## Getting stuck
>
> Now that we have introduced file editing and `echo`, you may encounter times when commands do not seem to work. Check
> your prompt.
> 
> If it has changed from `$` or `%` to `>` and running commands doesn't seem to work anymore, it is likely caused by an
> unclosed quote `"` or `'`. The simple keyboard fix for this is `Ctrl+C` which will cause the shell to exit out of the
> command that you are typing.
> 
{: .callout}

Now, how can we view it? We use a command, `cat`, short for concatenate to view the contents of the file.

~~~
$ cat correct.txt
~~~
{: .language-bash}

~~~
this correct message
~~~
{: .output}

As you can see, it prints the output of the file to the terminal output. On Linux systems themselves, you can type
`tac`, which will do the reverse.

Most of the time though, files tend to be
longer than a line. So, there is another command called `less` which opens a new window in which you can view the file.
You can exit by pressing `Q`, and search for a word using `/word`. Let's try for `hamlet.txt`, which is several
thousand lines long.

~~~
$ less hamlet.txt
~~~
{: .language-bash}

The command `more` oddly enough, is not as useful, but also an option to view files. It combines the use of `less` with
pressing `Q` to exit, and `cat` by printing to the screen.

There are another couple of useful commands, `head` and `tail`, which by default print the first and last 10 lines of a
file to the screen respectively. You can specify the number of lines by adding a `-n` flag.

~~~
$ head hamlet.txt
~~~
{: .language-bash}

~~~
THE TRAGEDY OF HAMLET, PRINCE OF DENMARK


by William Shakespeare



Dramatis Personae

  Claudius, King of Denmark.
~~~
{: .output}

~~~
$ tail -n 5 hamlet.txt
~~~
{: .language-bash}

~~~
Exeunt marching; after the which a peal of ordnance
                                                   are shot off.  


THE END

~~~
{: .output}

> ## Familiarisation with "viewing" commands
>
> Spend a few minutes familairising yourself with the commands, `head`, `tail`, `less`, `more`, `cat`. Which do you
> feel works better in certain situations. Why?
> 
{: .challenge}

## Spot the difference with `diff`

We now move onto analysing the difference between files with the `diff` command. This compares one file to another to
ensure they are the same.

When we type the following command to compare our two files.

~~~
diff correct.txt incorrect.txt
~~~
{: .language-bash}

The `<` corresponds to the first file entered, in this case `correct.txt`, and the `>` corresponds to the second file.
It will produce the following output.

~~~
1c1
< This message is correct
---
> This message is incorrect
~~~
{: .output}

The `1c1` highlights the lines that are different and what needs changing. This can be very helpful if you are looking
at two very similar files.

Let us change our files `incorrect.txt` and `correct.txt` with `echo` and see the resulting difference with `diff`.

We can press `Enter` before closing our quotes to spread the message onto the next line. You will notice something is
different when the prompt changes.

~~~
$ echo "This message is correct" > incorrect.txt
$ echo "This message is correct
> but not as correct as this." > correct.txt
~~~
{: .language-bash}

Now we will use `diff` again to see what has changed.

~~~
diff correct.txt incorrect.txt
~~~
{: .language-bash}

~~~
2d1
< but not as correct as this.
~~~
{: .output}

We see that the output `2d1` is telling us to delete a the second line in our file `correct.txt` to make it the same as
`incorrect.txt`.

So having the order right is important. The best way to describe `diff` is **How can I change file 1 to make it the** 
**same as file 2?**

If we reverse the command, it will tell us to add a line to `incorrect.txt` to make it the same as `correct.txt`.

~~~
diff incorrect.txt correct.txt
~~~
{: .language-bash}

~~~
1a2
> but not as correct as this.
~~~
{: .output}

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
$ touch new.txt
$ gzip new.txt
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
file `f` flags, as well as specitfying a name for the tar archive. You can also add the verbose flag (`v`), which lists
the files that are being added.

~~~
$ tar -cf archive.tar new.txt
~~~
{: .language-bash}

If we check our directory, we can see that the original file, plus the tar archive itself are now present. Because this
is now an archive, not a directory, we cannot check its contents. Luckily there is a flag (`t`) that we can use to view
the archive contents. 

~~~
$ tar -tf archive.tar
~~~
{: .language-bash}

~~~
new.txt
~~~
{: .output}

As you can see, it lists out the contents of the archive in the same way that `ls` lists out the content of a directory.

Let us remove the original file, `new.txt` and then extract the contents of our `.tar` archive using the `x` flag.

~~~
$ rm new.txt
$ tar -xf archive.tar
~~~
{: .language-bash}

Running our `ls` command will confirm that `new.txt` has returned to the directory by extracting the file. You can
remove `.tar` archives using the `rm` command.

> ## `tar`-ing and `gzip`-ing a directory 
>
> Use `tar` plus its flags to create a `.tar` archive of the `wildcards/` directory. Check the contents of the archive.
> Now zip the archive using `gzip`.
> 
> Finally, unzip and untar the archive.
> 
>
> > ## Solution
> >
> > ~~~
> > $ tar -cf my_archive.tar wildcards/
> > $ tar -tf my_archive.tar
> > ~~~
> > {: .language-bash}
> >
> > ~~~
> > wildcards/
> > wildcards/01.txt
> > wildcards/00.txt
> > wildcards/02.txt
> > wildcards/07.txt
> > wildcards/06.txt
> > wildcards/10.txt
> > wildcards/11.c
> > wildcards/04.c
> > wildcards/08.txt
> > wildcards/03.c
> > wildcards/09.txt
> > ~~~
> > {: .output}
> > 
> > ~~~
> > gzip my_archive.tar
> > gunzip my_archive.tar.gz
> > tar -xf my_archive.tar
> > ~~~
> > {: .language-bash}
> > 
> {: .solution}
{: .challenge}

## Wildcards

Now we will get to use the `wildcards/` directory we were referencing in the previous exercise

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
to the right, which is divided into three sections, user, group and other.

The first section above has the three characters `rw-`, which indicates that the user can read and write content to the
file. The permission can be changed so that the file can be executed or run, however we will come to that shortly.

The second section `r--` refers to the group owner, i.e. a group on a machine. Here the `w` has been replaced with a
`-` indicating that the group has read-only permissions. This is a similar case for the third section, also `r--`,
which indicates that others have read-only permissions.

Who cares you may ask. Well, a common occurrence is that people on a project or a course would need to
share and edit files,or need to access materials from a directory outside of their account. As things stand, this is
not possible, but by changing permissions, this is possible.

We can change the permissions of a file using `chmod` along with a variety of flags which can add or take away file
permissions. Let's change the permissions of our `correct.txt`, then use `echo` to write to the file.

~~~
$ chmod u-w correct.txt
$ echo "new line" > correct.txt
~~~
{: .language-bash}

~~~
permission denied: correct.txt
~~~
{: .output}

As you can see, because we have changed permissions, we cannot edit the file anymore.

Let us change the permissions, but add writing permissions to all users (user, group, other)

~~~
$ chmod ugo+w correct.txt
~~~
{: .language-bash}

Now when we check the permissions with `ls -lh` we can see that the permissions have changed to;

~~~
-rw-rw-rw-
~~~
{: .output}

> ## Changing file permissions
>
> You may need to change the permissions of a file so group users can edit, or execute the file.
> 
> Create a new file, `my_script.sh`, which should automatically have the permissions `-rw-r--r--`. Check yourself that
> the file has these permissions, then;
> 1. Add executable permissions for user and group
> 2. Remove reading permissions for other
>
> > ## Solution
> >
> > ~~~
> > $ chmod ug+x my_script.sh
> > $ chmod o-r my_script.sh
> > ~~~
> > {: .language-bash}
> {: .solution}
{: .challenge}

There are also number notations corresponding to `u`, `g` and `o` read, write and executable permissions, as shown in
the table below. 

| Character | Number Notation | Character | Number Notation |
|-----------|-----------------|-----------|-----------------|
|   `---`   |        0        |   `r--`   |        4        |
|   `--x`   |        1        |   `r-x`   |        5        |
|   `-w-`   |        2        |   `rw-`   |        6        |
|   `-wx`   |        3        |   `rwx`   |        7        |

These numbers are read in as a three character long binary number, read from right to left. The below example shows how
the numbers can be summed up, so that;
1. The owner can read, write and execute the file
2. The group can read and execute the file, but not edit it
3. All others cannot read, write or execute it

~~~
OWNER  GROUP  OTHER
r w x  r w x  r w x
1 1 1  1 0 1  0 0 0
  7      5      0
  |______|______|
         |
        750
~~~
{: .output}

If we wanted to change a file's permissions to match the above, we can do so using;

~~~
$ chmod 750 my_script.sh
~~~
{: .language-bash}

> ## Who has what permissions?
> 
> Have a look at the different `rwx` permissions and numerical equivalents, and deduce who has what permissions, or who
> has been granted, or had permissions retracted
>
> 1. `rwxrwxr--`
> 2. `r--r--r--`
> 3. `755`
> 4. `700`
> 5. `rwxrw-r--`
> 6. `chmod u+x file`
> 7. `chmod go-wx file`
>
> > ## Solution
> >
> > 1. **User** and **group** can *read*, *write*, *execute*. **Other** can only *read* the file.
> > 2. **User**, **group** and **other** can only *read* the file
> > 3. **User** can *read*, *write* and *execute* the file. **Group** and **other** can *read* and *write* the file.
> > 4. **User** can *read*, *write* and *execute* the file, **group** and **other** cannot do anything.
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
