---
title: "Extra commands"
teaching: 5
exercises: 10
questions:
- "How can I search for a string in a file"
- "What are pipes and how do they work?"
- "What are sed and awk?" 
- "How can I see the differences between two files?"
- "How can I zip files?"
- "What are `.tar` archives?"
objectives:
- "Be able to observe differences between files using `diff`"
- "Create and work with `.zip` files and `.tar` archives"
- "Understand the benefits of searching and using pipes"
keypoints:
- "`grep` selects lines in files that match patterns. It can be combined with pipes `|` to be even more useful."
- "`.tar` archives are very useful ways of converting a while folder into a single file. They are often used in data
  sharing."
- "The creation of `.tar` archives requires the use of flags to create and untar them."
- "The `-cf` tar flags create an archive with a specified name. The `-xf` flag is used to extract the archive contents."
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## Searching 

We will now look into one of the most useful tools in Linux. There is possibly enough material on this command for a
whole episode, but we will keep it simple here.

The command for searching is `grep`, which stands for **globally search for a regular expression**. In English, it is
used to search for a string of characters in a specified file.

Let's use `grep` to search for all lines in `hamlet.txt` that contain the word "hamlet".

~~~
$ grep 'hamlet' hamlet.txt
~~~
{: .language-bash}

You will notice running this that nothing has happened. We therefore need to use a case insensitive flag (`i`) to get
this working, we will also add in the display line occurrence flag (`n`). Case sensitivity is important in `grep`

~~~
$ grep -i "hamlet" hamlet.txt
~~~
{: .language-bash}

As you can see, it produces a long output. But where grep really comes in useful is with pipes.

Pipes work on the concept that it is better to combine smaller commands into a more powerful and useful one. They can
also help remove unnecessary temporary files, and sends the output of one command to another. The syntax is;

`command_1 | command_2 | ... | command_n`

Let's work on this by piping the output of our previous command to `less`.

~~~
$ grep -i "hamlet" hamlet.txt | less
~~~
{: .language-bash}

On the output we can see that our `less` window has opened up. Remember you can type `Q` to exit. 

> ## Piping Hamlet to a file
>
> Use `grep` and `|` to choose a word, "Hamlet", "Ghost", "Queen" or another of your choosing and pipe it to a new
> file.
>
> > ## Solution
> >
> > ~~~
> > $ grep -n "Hamlet" | hamlet_occurrence.txt
> > ~~~ 
> > {: .language-bash}
> >
> {: .solution}
{: .challenge}

## Spot the difference with `diff`

We now move onto analysing the difference between files with the `diff` command. This compares one file to another to
ensure they are the same.

When we type the following command to compare our two files.

~~~
$ diff correct.txt incorrect.txt
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
$ diff correct.txt incorrect.txt
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
$ diff incorrect.txt correct.txt
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
$ gunzip new.txt.gz
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
over multiple lines.

{% include links.md %}
