---
title: "ssh Keys"
teaching: 10
exercises: 0
questions:
- "What is ssh and the secure shell?"
- "How does an ssh key work?"
- "What is the difference between a public and private key"
- "Why do I need an ssh key?"
- "How do I create an ssh key on different operating systems"
- "How do I log into a supercomputer?"
objectives:
- "Introduce the concepts of ssh keys and why they are needed"
- "Generate an ssh key-pair for different operating systems"
keypoints:
- "ssh key-pairs are needed to log into most supercomputing systems"
- "To log into ICHEC's cluster, an ssh key-pair is necessary"
- "You only need one ssh key-pair generated per device"
- "ssh keys are typically stored in the user's home directory"
---

<p align="center"><img src="../fig/ICHEC_Logo.jpg" width="40%"/></p>

## What is SSH?

SSH, also known as the Secure Shell or Secure Socket SHell is a network protocol that gives users, and in particular
system administrators a secure way to access a computer over an unsecured network.

A supercomputer, and the cloud is a group of system nodes that can be found at a specific location. Although it would 
be technically possible to access these locations and plug your own computer into the machine and do the work you need
it is a very impractical solution. Therefore a way of accessing the computer over networks that are not secure is 
necessary, and SSH is an ideal way in which to do so.

It also refers to the utilities that come with it as a result. In implementing SSH, one provides a password and public 
key authentication, as well as encrypted data communications between two computers over open networks like the internet.

Enabling an ssh key on your device can enable you to connect to a supercomputer in your office, at home, or even on a
beach provided you have a form of internet connection.

SSH can also be used to create secure "tunnels" for application protocols, and these are usually graphical sessions
such as JupyterHub. On ICHEC systems, an ssh connection through a tunnel is needed to access JupyterHub.

## How does an SSH key work?

An SSH key can be thought of like a bar code on an ID tag. The ID tag itself contains other information, such as your
name, the company, age, gender, profile pictures and other information. When you go up to a locked door, and present 
your ID, the scanner checks the barcode on your ID tag to see if it matches the data that it has on the system. If it 
is a match, then you are granted access to the building/room. If you present a different or expired card, the ID tags 
will not match and therefore you are unable to access the system.

SSH keys work in exactly the same way, except you have to generate the keys yourself rather than having a security 
person simply give you a key card. In the same way that the ID card authenticates your identity, the SSH key 
authenticates the identity of your computer.

When you generate an SSH key, you end up creating what is known as an SSH key-pair. It creates two different ones, one
being a public key, the other is a private key. 

We will come onto generating SSH keys later, 

###
###

## Public and Private keys

When you set up an SSH key, you generate a "key-pair", a **public** and **private** key. 

The public key, in cryptographic terms is a large numerical value that is used to encrypt data. Most people don't need 
to worry about it, however it is important to know what is looks like when printed to the screen. Public keys will have 
the extension `.pub`.

The private key, which is generated alongside the public key must stay on your local machine and not shared with anyone.
These are used to decrypt messages that were created with the corresponding public key or to create signatures.

In other words, a public key locks up data from unauthorised use, while a private key is used to unlock it. The machines
perform a virtual handshake

> ## Create your own SSH key-pair: Part 1
>
> What do you need to do once you have created an SSH key pair, and you want to have access to a supercomputer
> 
> 1. Submit my private key, as the account on the remote system will be private to me, and is needed to perform the
>    virtual handshake
> 2. Submit my public key, as the remote system needs it to perform the virtual handshake
> 3. I don't need to do anything, as I have both of them. The remote system only needs to acknowledge that my machine 
>    exists.
> 4. Submit both my public and private keys, as both will be needed for me to log in and for the machines to perform a
>    virtual handshake
> 5. Generate a new SSH key pair in a different directory
>
> > ## Solution
> >
> > 1. No. Your private key should stay on your computer and not be shared with anyone.
> > 2. Yes. The systems team or framework will be able to add your ssh key to your account.
> > 3. No, the helpdesk team will still need your public key for you to gain access to the system.
> > 4. No, only the public key is needed for the virtual handshake.
> > 5. No, you only need one ssh key-pair per machine.
> {: .solution}
{: .challenge}


## Generating an SSH key-pair

The process of setting up an SSH key-pair is relatively simple on Mac and Linux operating systems, but is not as simple 
on Windows. Depending on your terminal emulator, it can put your SSH key in odd places.

SSH keys typically have a location in a hidden folder in your home directory. Until you create an SSH key-pair for the
first time this directory, `.ssh` will not exist.

There are many different SSH key types, depending on the algorithm use to generate it. This includes `rsa`, `ed25519`, 
which have different levels of encryption. Here we will be creating a key with 

> ## Create your own SSH key-pair: Part 2
>
> 1. Navigate to your home directory and execute the following command.
>
> `ssh-keygen -t ed25519`
> 
> 2. You can then accept the default filename and location for your key-pair, by pressing either `Enter` or `Return`
> 3. Enter a password which you can remember (or alternatively leave it blank), and again press `Enter` or `Return`.
>    In addition to a course or project account, you will need to enter this password every time you log in.
> 
{: .challenge}

## How can I log into a supercomputer

By now we have created an SSH key-pair, let's try and log in using the command;

`ssh USERNAME@machine.example.com`

Here, the `USERNAME` corresponds in this case to your course account number, the `machine` is Kay, and `example.com` 
refers to `ichec.ie`. Think of it like an email address, you can't send information to anyone without their username
or the domain name (gmail, yahoo, institution)

> ## Logging into Kay
>
> Now using the course account given to you, try and log in by adapting the command above. You will need the password
> that you generated whilst creating your SSH key.
>
> > ## Solution
> >
> > You should have got an error saying `Permission denied (publickey)`. 
> > 
> > This occurs when your public key has not been added to your account, and is a very common problem that users can
> > encounter. This is not something that you can control as the systems team need to manually link it to the
> > account you are using. Users are not allowed on an HPC with an SSH key alone. At ICHEC, you need to have a project 
> > to join or be partaking in one of our courses to gain access.
> >
> > To gain access, you will need to send your public SSH key either as a ticket to systems, or in this lesson, via a 
> > webform which will be posted to you in the chat.
> >
> {: .solution}
{: .challenge}

If you are joining us for our intro-to-hpc course, you will be granted access to Kay and have some time to work on some
problems.

For now however we can inform you of the next steps.

Once your SSH key has been added, the error message you have experienced will be replaced by a block of text similar to
below. 

```bash
The authenticity of host 'sample.ssh.com' cannot be established.
 DSA key fingerprint is 01:23:45:67:89:ab:cd:ef:ff:fe:dc:bb:98:76:54:32:10.
 Are you sure you want to continue connecting (yes/no)?
```

By typing yes, you are accepting the remote machine as a known host. You can then continue logging in. You would 
eventully need to provide your ssh key password and a course account password.

Thise taking the intro-to-hpc course will be provided this information on Monday following the submission of an SSH key.

{% include links.md %}
