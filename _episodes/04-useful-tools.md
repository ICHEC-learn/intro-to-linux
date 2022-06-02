---
title: "Useful Tools"
teaching: 25
exercises: 15
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

## Wildcards

Wildcards are one of the most useful tools in Linux and can be used to substitute any character(s) in a command.

Let's look into their uses. Ensure that you are in the `test` directory, and lets create a few files.

~~~
$ touch 001.txt 002.txt 003.c 004.py 101.txt 211.py
~~~
{: .language-bash}

Let's use the most useful one first, `*`, which implies **everything**. If we type `ls *`, it will not be very useful
as it will list all the contents of a directory, which `ls` does anyway. Let's see what happens if we select only
certain file types, by using `*` followed immediately with `.txt` with no whitespace.

~~~
$ ls *.txt
~~~
{: .language-bash}

~~~
001.txt		002.txt		correct.txt	hamlet.txt	incorrect.txt
~~~
{: .output}

We only get the files with that extension. It can work in reverse as well, we can only select the files that start with
`0`.

~~~
$ ls 0*
~~~
{: .language-bash}

~~~
001.txt	002.txt	003.txt	004.py
~~~
{: .output}

Now, we can see that all the files starting with `0` have been added, regardless of the extension.

We move now onto the `?` wildcard, which will replace a single character rather than all of them.

~~~
$ ls 00?.txt
~~~
{: .language-bash}

~~~
001.txt	002.txt	003.txt
~~~
{: .output}

In comparison to our previous command, only the three files have been seelcted. We can use the `?` more than once in a
command, as shown below, as our `101.txt` file can also be selected.

~~~
$ ls ?0?.txt
~~~
{: .language-bash}

~~~
001.txt	002.txt	101.txt
~~~
{: .output}

Our final wildcard is `[]`, which signifies a collection of possible values, which is more specific than `?`. We can
specify the exact numbers we want to display. Let's select the odd numbers.

~~~
$ ls 00[13].txt
~~~
{: .language-bash}

~~~
001.txt	003.txt
~~~
{: .output}

> ## Danger with wildcards
>
> These are incredibly useful tools and having a good mastery of these is crucial, particularly with `*` as it can be 
> very easy to remove a bunch of files by accident!
>
{: .callout} 

> ## Practice using wildcards
>
> Now we will get to use the `wildcards/` directory we were referencing in the previous exercise. Practice using
> the different wildcards to remove, or list out the different files. Remember you can use `touch` to create a new
> empty file.
> 
> Try combining two or more wildcards (`*`, `[]`, `?`) in the same command. Is the output what you would expect?
>
{: .challenge}

{% include links.md %}