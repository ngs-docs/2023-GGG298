---
tags: ggg, ggg2023, ggg298
---

# Week 3 lab notes - GGG 298 - Jan 25, 2023

[![hackmd-github-sync-badge](https://hackmd.io/4Tm5i97QT5iDlZL-IC7U8A/badge)](https://hackmd.io/4Tm5i97QT5iDlZL-IC7U8A)

[Permanent link](https://github.com/ngs-docs/2023-GGG298/blob/main/lab-3.md)

TODO:
* post to canvas
* resolve @@

[toc]

## Today!

Today will be scattered across multiple topics, but hopefully this will be the last super-scattered lesson. I'll post a topics schedule for the rest of the quarter shortly, but most of the remaining lab sessions will focus on specific topics, with a few hands-on practice sessions in the middle.

Rough outline:

* logging into farm and running RStudio Server from Windows and Mac.
* working on multiuser systems - a brief intro
* UNIX commands more generally - cd, ls, rm, files and folders, and commands
* running the sourmash workflow on farm - what are all the steps?
* what is sourmash doing "underneath" - a brief introduction to k-mer comparisons and Jaccard similarity *(if we have time)*

## Logging into farm

Revisit [week 2 notes on logging into farm](https://hackmd.io/n7_pXRiiRQ-YpQBQ93uW9Q?view#1-Logging-into-farm)

## Running RStudio Server

Revisit [week 2 notes on running RStudio Server](https://hackmd.io/n7_pXRiiRQ-YpQBQ93uW9Q?view#2-Start-and-connect-to-an-RStudio-Server-on-farm)

Step by step - what is happening here?
* logging in to farm (first time)
* srun command
* modules command
* rserver-farm
* logging in again with ssh
* connecting to RStudio Server 

### ssh "tunneling" - what is happening?

![](https://hackmd.io/_uploads/SkgsZxJ2i.png)

* farm head node doesn't run big compute jobs, so you can't run RStudio there
* farm compute nodes are "hidden" from the Internet, so you can't connect directly to them
* so you tell ssh to "tunnel" from your laptop through farm head node to the farm compute nodes

It's actually kind of astonishing that it works... but it generally does!

Question: why do you need two ssh connections to farm?? Why can't we do all of the commands in one!?

## UNIX commands: a brief introduction

Adapted from: [Introduction to the UNIX Command Line](https://ngs-docs.github.io/2021-august-remote-computing/introduction-to-the-unix-command-line.html)

### Learning Goals
* visualize file/directory structures
* understand basic shell vocabulary
* gain exposure to the syntax of shell & shell scripting
* look at the contents of a directory 
* commands: `pwd`, `ls`, `cd`

------------------------------------

#### What is the shell and what is the terminal?

The **shell** is a computer program that uses a command line interface (CLI) to give commands made by your keyboard to your operating system. Most people are used to interacting with a graphic user interface (GUI), where you can use a combination of your mouse and keyboard to carry out commands on your computer. We can use the shell through a **terminal** program. 

Everything we can do using our computer GUI, we can do in the shell. We can open programs, run analyses, create documents, delete files and create folders. We should note that _folders_ are called **directories** at the command line. For all intents and purposes they can be used interchangeably but if you'd like more information please see "The folder metaphor" section of [Wikipedia](https://en.wikipedia.org/wiki/Directory_%28computing%29#Folder_metaphor).

The ease of getting things done via the shell will increase with your exposure to the program.  

### Preparation

To get started with this section,

* open a terminal window (in ssh or with RStudio)
* run:

```
cd
wget https://s3-us-west-1.amazonaws.com/dib-training.ucdavis.edu/shell-data.zip
unzip shell-data.zip
```
This will preload some data that we will explore.

### Starting at the shell.

When we open up the terminal and/or connect to farm with ssh, we will see a line of text. This is a **prompt statement**. It can tell us useful things such as the name of the directory we are currently in, our username, or what computer we are currently running terminal on.

Let's take a look around. First, we can use the **print working directory** command see what directory we are currently located in.

```
pwd
```

This gives us the **absolute path** to the directory where we are located. An absolute path shows the complete series of directories you need to locate either a directory or a file starting from the root directory of your computer.

What is the root?
A useful way to start thinking about directories and files is through levels. At the highest level of your computer, you have the **root directory**. Everything that is contained in your computer is located in directories below your root directory. 
![CLIvsGUI](https://github.com/ngs-docs/2021-august-remote-computing/blob/main/CLIvsGUI.png?raw=true)


We can also look at the contents of the directory by using the `ls`
("list") command:

```
ls
```

This command prints out a list of files and directories that are located in our current working directory. Let's look at the subdirectory `data/`.

To change the working directory, we need to use the `cd` ("change
directory") command. Let's move into the data directory.

```
cd data
```

Let's have a look around.

```
ls
```

We can see the following files:

> > ~~~
> > MiSeq		Slide1.jpg	hello.sh	nano1.png
> > README.md	gvng.jpg		nano2.png
> > ~~~
However, this directory contains more than the eye can see! To show hidden files we can use the `-a` option.

```
ls -a
```

We will see the following:

> > ~~~
> > .		MiSeq		Slide1.jpg	hello.sh	nano1.png
> > ..		README.md	gvng.jpg	.hidden		nano2.png
> > ~~~
Three new items pop up `.`, `..` and `.hidden`. 

Using options with our commands allows us to do a lot! But how did we know to add `-a` after ls? Most commands offer a `--help`. Let's look at the available options that `ls` has:

```
ls --help
```

Here we see a long list of options. Each option will allow us to do something different.

For example,
```
ls -F
```
will give indicators as to whether something is a file, a directory, or whatever.

We can also combine commands:

```
ls -aFl
```

This combination of options will _list_ _all_ the contents of the directory and _differentiate_ between file types.

### Navigation

#### Learning Goals
* paths
* look at the contents of files
* perform functions outside of the directory you are in
* intro to the wildcard expression: `*`
* copy, move and remove files
* create and remove directories
* understand the structure of commands
* commands: `cat`, `cp`, `mv`, `rm`, `mkdir`

--------------------------------------------

Now we have seen how to navigate around our computers and seeing what is located in the directory we are in. But some of the beauty of the shell is that we can execute activities in locations that we are not currently in. To do this we can either use an absolute path or a relative path. A **relative path** is the path to another directory from the the one you are currently in. 

Navigate into the `tmp1` directory located in the `.hidden` directory.

```
cd .hidden/tmp1
```

Here we see two files `notit.txt` and `thisinnotit.txt`. We can see what is in the directories using the `cat` command which concatenates and prints the content of the file we list. 

```
cat thisinnotit.txt
```

> > ~~~
> > This is not the text file you're looking for
> > ~~~
NOTE - you can use TAB to do filename completion, so if you type `cat this` and then press your Tab key once, it will autocomplete if there is a unique match. If there is more than one match, the first Tab will do nothing, and the second will show all the possible matches.

Let's see what else is in the other tmp directories:

```
ls ../tmp2
```

and we can see the contents of tmp3

```
ls ../tmp3
```

So, even though we are in the `tmp1/` directory, we can see what is in other directories by using the relative path to the directory of interest. Note we can also use absolute paths too. You may have noticed the `../` this is how to get to the directory above the one you are currently located in. 

Note: in this case, we have access to the RStudio file browser, too, which is really nice. But in the future we won't. So we can use the file browser today, but on Farm we'll have to get by with just the command line interface and no other interface!

**CHALLENGE:** Use the absolute path to list the files in the tmp2 directory.

Wouldn't it be nice to see the contents of all the tmp directories at once? We can use a regular expression to capture a sequence of characters (like the numbers 1, 2 and 3 at the end of the tmp directories). We can use the wild card character `*`, which expands to match any amount of characters.

```
ls ../tmp*
```

> > ~~~
> > ../tmp1:
> > notit.txt	thisinnotit.txt
> > 
> > ../tmp2:
> > anotherfile.txt
> > 
> > ../tmp3:
> > closebutnotit.txt	youfoundit.txt
> > ~~~
So, even though we are in the `tmp1` directory we can use a relative path.

We are quite used to moving, copying and deleting files using a GUI. All of these functions can be carried out at the command line with the following commands: 

Copy files with the `cp` command by specifying a file to copy and the location of the copied file. Here we will copy the `thisinnotit.txt` into the file `thisisacopy.txt`. 

```
cp thisinnotit.txt thisisacopy.txt
```

The syntax for the copy command is `cp <source_file> <destination_file>`. Using this syntax we can copy files to other directories as well:

```
cp thisinnotit.txt ../tmp2
```

If we navigate to the tmp2 directory and list the files that are in it we will see the `thisinnotit.txt` file has been copied to the tmp2 directory.

```
cd ../tmp2
ls -l
```

**CHALLENGE:** Use the `mv` command to move the `thisinnotit.txt` file from tmp2 to tmp3.

Once we know how to copy and move files, we can also copy and move directories. We can create new directories with the command `mkdir`. Let's make a new directory called `tmp4`

```
cd ../
mkdir tmp4
ls -l
```

The shell is quite powerful and can create multiple directories at once. It can create multiple directories in the current working directory:

```
mkdir tmp5 tmp6
ls -l
```

or it can create a series of directories on top of one another:

```
mkdir -p how/deep/does/the/rabbit/hole/go
```

We can use tab complete to get to the `go` directory. Type `cd h` then hit <kbd>tab</kbd>. If you hit tab enough times your command will eventually read:

```
cd how/deep/does/the/rabbit/hole/go/
```

You can see that we've created a bit of a monster directory structure...

**CHALLENGE:** Navigate to the data directory and use the `rm` command to remove the `how` directory and all its contents. 

----

This nicely hints at the power of the shell - you can do certain things (in this case, create a nested hierarchy of directories) much more easily in the shell. But that power cuts both ways - you can also mess things up more easily in the shell!

### Some final notes on this section

This lesson focused on file and directory exploration because that's
something everyone needs to know, and all these commands will work on
pretty much any computer that is running a UNIX compatible shell (including
Mac OS X and Windows Subsystem for Linux).

Google (and especially stackoverflow) is your friend! Use Internet
search whenever you have questions about what a command does, or what
commands to use to achieve a particular tasks.

## Working on multiuser systems like farm

(Adapted from [Running programs on remote computers and retrieving the results](https://ngs-docs.github.io/2021-august-remote-computing/running-programs-on-remote-computers-and-retrieving-the-results.html).)

### Using multiple terminals

You don't have to be logged in just once!

On Mac OS X, you can use Command-N to open a new Terminal window, and then
ssh into farm from that window too.

On Windows, you can open a new connection from MobaXterm simply by double
clicking your current session under "User sessions."

In RStudio Server, you can open a second Terminal.

What you'll end up with are different command-line prompts on the same
underlying system.

They share:

* directory and file access (filesystem)
* access to run the same programs, potentially at the same time

They do not have the same:

* current working directory (`pwd`)
* running programs, and stdin and stdout (e.g. `ls` in one will not go to the other)
* activate module or conda environments (more on this later)

These are essentially different _sessions_ on the same computer, much like
you might have multiple folders or applications open on your Mac or Windows
machine.

You can log out of one independently of the other, as well.

And you can have as many terminal connections as you want! You just have
to figure out how to manage them :).

### Who am I and where am I running!?

If you start using remote computers frequently, you may end up logging
into several different computers and have several different sessions
open at the same time. This can get ...confusing!

There are several ways to help track where you are and what you're doing.

One is via the command prompt. You'll notice that on farm, the command
prompt contains three pieces of information by default: your username,
the machine name ('farm'), and your current working directory!  This is
precisely so that you can look at a terminal window and have some idea
of where you're running.

You might also find the following commands useful:

This command will give you your current username:
```
whoami
```

and this command will give you the name of the machine you're logged
into:
```
hostname
```

These can be useful when you get confused about where you are and who
you're logged in as :)

### Looking at what's running

You can use the `ps` command to see what your account, and other accounts,
are running:
```
ps -u datalab-02
```

This lists all of the different programs being run by that user, across
all their shell sessions.

The key column here is the last one, which tells you what program is
running under that process.

You can also get a sort of "leaderboard" for what's going on on the shared
computer by running
```
top
```
(use 'q' to exit).

This gives a lot of information about running processes, sorted by who is
using the most CPU time. If the system is really slow, it may be because
one or more people are running a lot of things, and `top` will help you
figure out if that's the problem.

---

This is one of the consequences of having a shared system. You have
access to extra compute, disk, and software that's managed by
professionals (yay!), but you also have to deal with other users
(boo!)  who may be competing with you for resources. We'll talk more
about this when we come to the Slurm class, where
we talk about bigger analyses and the SLURM system for making use of
compute clusters by reserving or scheduling compute. (You're already doing this with srun.)

## Running the sourmash workflow on farm

What are the commands doing?

Step by step:
* git clone
* mamba and conda commands
* snakemake
* file transfer options

How to _reconnect_:

* change to the right directory
* activate the relevant conda environment

### Let's practice:

We'll just start doing this regularly in class, so it's worth getting it down to a routine :)

* close down everything (ssh, rstudio, terminal, etc.)
* start terminal & ssh connection
* srun, module load, rstudio server
* (separate window) ssh tunnel
* open RStudio Server in web browser
* conda activate
* change directory
* run snakemake

Command reference:
```
# allocate a compute node
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 1 --mem 5GB --pty /bin/bash

# load R and RStudio Server modules
module load spack/R/4.1.1
module load rstudio-server/2022.07.1

# run RStudio on node
rserver-farm
```

Inside RStudio:
```
# go to right directory/folder
cd
cd 298-compare

# activate the set of software
conda activate lab2

# run snakemake
snakemake -j 1
```

### Diagnosing common problems

#### I can't find my files!

You're probably in the wrong working directory if:

* `ls` doesn't show you the files you expect to see
* `pwd` doesn't give the right directory

solution: type `cd ~/`, `ls`, and then look for right directory; then `cd` into it.

#### You're trying to run a command, and it's saying 'command not found!'

If you try to run snakemake and it says "command not found", you're probably not in the right conda environment.

The conda environment is listed in the first part of your prompt; see:
```
(base) datalab-02@farm:~$ 
 ^^^^
```

the 'base' here means you're in the conda environment named 'base'. You probably want to be in the conda environment called 'lab2':
```
conda activate lab2
```

#### It tells you you can't run RStudio Server!

If you run `module load rstudio-server/2022.07.1` and see: `RStudio Server is not allowed on the head node.` then you forgot to do the srun to allocate yourself a compute node!

## What is sourmash actually doing underneath?

See [rendered notebook](https://sourmash.readthedocs.io/en/latest/kmers-and-minhash.html).

sourmash details to discuss -
* `sourmash sketch dna` - extracts k-mers
* `sourmash compare` - loads all k-mers, compares
* `sourmash plot` - plots relationship

sourmash uses a "subcommand" format for many things, e.g. `sketch`.

* options - long and short
* how to find out more:
    * documentation
    * `-h/--help`
    * google

## Log out/disconnect/close things

CTRl-C to kill rstudio server process

`exit` to exit the compute node srun shell

