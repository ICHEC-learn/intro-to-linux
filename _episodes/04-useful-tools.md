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

## Wildcards

`* ? [] *?[]`

## File permissions

`chmod`

## Searching 

`grep` + pipes

## `sed` and `awk` sub-languages

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
