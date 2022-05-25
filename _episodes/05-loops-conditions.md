---
title: "Loops and Conditionals"
teaching: 10
exercises: 0
questions:
- "How can I perform the same actions on many different files?"
objectives:
- "Write a loop that applies one or more commands separately to each file in a set of files."
- "Explain the difference between a variable's name and its value."
keypoints:
- "A `for` loop repeats commands once for every thing in a list."
- "Every `for` loop needs a variable to refer to the thing it is currently operating on."
- "Use `$name` to expand a variable (i.e., get its value). `${name}` can also be used."
- "Do not use spaces, quotes, or wildcard characters such as '*' or '?' in filenames, as it complicates variable expansion."
- "Give files consistent names that are easy to match with wildcard patterns to make it easy to select them for looping."
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## Variables in Linux

When using variables it is also possible to put the names into curly braces to clearly delimit the variable
name: `$filename` is equivalent to `${filename}`, but is different from `${file}name`. You may find this notation in other 
people's programs.

They are nothing to be concerned about, but are mainly used in for loops which we will cover below and bash scripting.

There are some variables that already exist in bash, like `env`, or `HOME`. Some need the $ sign before it (such as
`$HOME`).

To access the contents of the variable `HOME` we can use `echo`.

~~~
$ echo $HOME
~~~
{: .language-bash}

~~~
/Users/johnsmith
~~~
{: .output}

## Loops

**Loops** are a programming construct which allow us to repeat a command or set of commands
for each item in a list. As such they are key to productivity improvements through automation.
They are similar to wildcards and tab completion, using loops also reduces the
amount of typing required (and hence reduces the number of typing mistakes).

Suppose we have several hundred genome data files named `basilisk.dat`, `minotaur.dat`, and
`unicorn.dat`. For this example, we'll use the `loops/` directory which only has three example files,
but the principles can be applied to many many more files at once.

The structure of these files is the same: the common name, classification, and updated date are
presented on the first three lines, with DNA sequences on the following lines.
Let's look at the files:

```
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```
{: .language-bash}

We would like to print out the classification for each species, which is given on the second line of each file.
For each file, we would need to execute the command `head -n 2` and pipe this to `tail -n 1`.
We’ll use a loop to solve this problem, but first let’s look at the general form of a loop:

```
for thing in list_of_things
do
    operation_using $thing    # Indentation within the loop is not required, but aids legibility
done
```
{: .language-bash}

and we can apply this to our example like this:

```
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $filename | tail -n 1
> done
```
{: .language-bash}

```
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```
{: .output}


> ## Follow the Prompt
>
> The shell prompt changes from `$` to `>` and back again as we were
> typing in our loop. The second prompt, `>`, is different to remind
> us that we haven't finished typing a complete command yet. A semicolon, `;`,
> can be used to separate two commands written on a single line.
{: .callout}

In this example, the list is three filenames: `basilisk.dat`, `minotaur.dat`, and `unicorn.dat`.
Each time the loop iterates, it will assign a file name to the variable `filename` and run the `head` command.
The first time through the loop, `$filename` is `basilisk.dat`. The interpreter runs the command `head` on 
`basilisk.dat` and pipes the first two lines to the `tail` command, which then prints the second line of 
`basilisk.dat`. For the second iteration, `$filename` becomes `minotaur.dat`. This time, the shell runs `head` on 
`minotaur.dat` and pipes the first two lines to the `tail` command, which then prints the second line of 
`minotaur.dat`. For the third iteration, `$filename` becomes `unicorn.dat`, so the shell runs the `head` command on
that file, and `tail` on the output of that. Since the list was only three items, the shell exits the `for` loop.

We have called the variable in this loop `filename` in order to make its purpose clearer to human readers.
The shell itself doesn't care what the variable is called. If we wrote this loop as:

~~~
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
~~~
{: .language-bash}

or:

~~~
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
~~~
{: .language-bash}

it would work exactly the same way. *Don't do this.* Programs are only useful if people can understand them,
so meaningless names (like `x`) or misleading names (like `temperature`) increase the odds that the program won't do
what its readers think it does.

> ## Conditionals
> 
> Conditional statements are also an option in bash, as well as functions. Although useful at times, we won't be
> spending too much time on them here as they are best saved for programming itself.
>
> The syntax for conditional statements in bash is as follows:
>
> ~~~
> if [ condition ] ; then
>   "do some stuff"
> fi
> ~~~
> {: .language-bash}
>
> | Integer comparison | String Comparison | Meaning                  |
> |--------------------|-------------------|--------------------------|
> |       `-eq`        |     `=` / `==`    | equal to                 |
> |       `-ne`        |        `!=`       | not equal to             |
> |    `-lt` / `<`     |         `<`       | less than                |
> |    `-le` / `<=`    |        `<=`       | less than or equal to    |
> |     `-gt` / `>`    |         `>`       | greater than             |
> |    `-ge` / `>=`    |        `>=`       | greater than or equal to |
>
> Depending on whether you are dealing with a string or integer, the following comparison may be useful for you.
> `["$a" -lt "$b"]` or `(("$a" < "$b"))`
> 
{: .callout}

{% include links.md %}
