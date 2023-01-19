---
tags: ggg, ggg2023, ggg298
---

# Week 2 lab notes - GGG 298 - Jan 18, 2023

[![hackmd-github-sync-badge](https://hackmd.io/n7_pXRiiRQ-YpQBQ93uW9Q/badge)](https://hackmd.io/n7_pXRiiRQ-YpQBQ93uW9Q)


[toc]

## Today!

This is an "on your own time" flipped-style lab, because (a) Titus has a conflict and (b) there will be a lot of individualized software install work.

Today's goals are to:

1. log into the farm cluster with a class account (5-30 min)
2. start and connect to an RStudio Server running on farm (5-30 min)
3. run the same genome comparison on farm (5 min)
4. be made aware of some of the resources available for working with the UNIX shell

See below for instructions, links, and videos to help you get through this all!

:::danger
Note: If you run into technical problems that prevent you from succeeding in any or all of this, that's fine - next week we will be able to use the binder. But by the first lab class in February we will switch over to farm completely so you will need to have your accounts sorted!
:::

## Important news and timely updates!

First discussion class will be tomorrow, Thursday, in Bainer 1128. Please be sure to read the paper and submit your answers to the question as per the canvas announcement!

## Reminder: Syllabus & links

The syllabus is [here](https://hackmd.io/Y3aIAoJsR_y-F-e2_UqZHw?view).

## 1. Logging into farm

### Account name and password.

You should have received an e-mail from me with an account name (datalab-xx) and password for logging into farm. You will need this information handy - I suggest putting it somewhere where you can copy and paste it!

:::info
FYI: If you already have an account on farm, I can help you get it set up to run things, BUT I would suggest not bothering since the datalab-xx accounts will work most easily. And, if/when the datalab-xx accounts don't work, it'll be my problem and not yours :).
:::

### Logging in with Mac OS X or Linux using the `ssh` program

See instructions [here](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#mac-os-x-using-the-terminal-program).

There is [a video](https://video.ucdavis.edu/media/Connecting+to+Remote+Computers+with+SSH/1_806ws8at) - start at 25m 08s.

### Logging in with Windows using MobaXTerm

See instructions [here](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#windows-connecting-to-remote-computers-with-mobaxterm).

There is [a video](https://video.ucdavis.edu/media/Connecting+to+Remote+Computers+with+SSH/1_806ws8at) - start at 35m 30s.

## 2. Start and connect to an RStudio Server on farm

Log in as above.

Your shell prompt should look something like this:
```
(base) datalab-05@farm:~$ 
```
This says you're logged into the farm head node (central computer) as account `datalab-05`; you're in your home directory (`~`); and the remote computer is ready to receive instructions.

#### Allocate a computer:

Now copy/paste the following command (both lines):
```
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 1 --mem 5GB --pty /bin/bash
```
you should see output like this:
```
srun: job 60489223 queued and waiting for resources
srun: job 60489223 has been allocated resources
```
(but with a different job number) and then your prompt will change to something like (but generally not the same as)
`(base) datalab-xx@c4-86`.

:::spoiler
Here, the `c4-86` is the name of one of the many compute nodes on farm.

The command above asks the farm cluster queuing system to find "room" for you on the cluster to run something for 3 hours on one CPU, using 5 GB of RAM.
:::

#### Load and run RStudio Server:

Now, load the RStudio Server module by running:
```
module load spack/R/4.1.1
module load rstudio-server/2022.07.1
```
and run the `rserver-farm` program:
```
rserver-farm
````
This will print out two things: a complicated looking command starting with `ssh`, and a Web site URL that starts with `localhost`. You'll need both of these!

An example:
:::spoiler
You need to use SSH tunneling to port forward from your desktop to RStudio Server.

Run the following command in a new terminal on your machine:

:::warning
ssh -L34468:c4-86:34468 datalab-02@farm.cse.ucdavis.edu

Then point your browser to http://localhost:34468

Username: datalab-02
Password: festival-bootie-capably-sedan-unheated-maker
:::

#### Start ssh tunneling:

Now, in a _new_ Terminal window (Mac OS X) or mobaxterm shell window (Windows) **on your laptop**, run the command it printed out for you to run - something like
```
ssh -L39XXX:c4-86:39XXX datalab-05@farm.cse.ucdavis.edu
```

and then go to the localhost URL (something like `http://localhost:39XXX`) in a browser.

You _should_ end up at an RStudio login page, where you can enter the username and password that were printed out when you ran `rserver-farm`.

:::warning
If this entire section fails at any point, that's ok - as long as you can log into farm, you can move onto the next step, it's just not as nice :). But we _do_ need to get this working for the following week, so please come prepared to debug things at the next lab session.
:::

## 3. Run the genome comparison workflow we looked at last week

Start a terminal session in RStudio, or, if you haven't gotten RStudio Server to work, by using ssh to connect to farm.

Mmake sure you're in your home directory:
```
cd ~/
```

Make a local copy of the github repository containing the workflow and put it in the directory `298-compare`:
```
git clone https://github.com/ngs-docs/2023-ggg298-sourmash-compare 298-compare/
```

Change your working directory into the new directory:
```
cd 298-compare/
```

Use `mamba` to install the required software in a conda environment named `lab2`:
```
mamba env create -f binder/environment.yml -n lab2
```
(This will take about 5-10 minutes to run.)

Activate the newly installed software environment so you can run software from it:
```
conda activate lab2
```

aaaaand run the pipeline:
```
snakemake -j 1
```

Now see if you can look at the figure produced by the workflow - it will be in the file `compare.mat.matrix.png`. 

If you are on RStudio Server, you can just click on the filename and it should open in a Web browser.

If you are on MobaXTerm, there should be a file browser you can use to look around the remote file system and transfer files back and forth.

If you are using `ssh` from a Terminal on Mac OS X, you'll have to copy it using `scp` or `sftp`. The remote pathname should be `datalab-xx@farm.cse.ucdavis.edu:298-compare/compare.mat.matrix.png` and so the command will be something like:
```
scp datalab-xx@farm.cse.ucdavis.edu:298-compare/compare.mat.matrix.png ./
```
See [this link](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html#copying-files-to-and-from-your-local-computer.) for a little more information.

## 3b. Logging out

It is polite to close sessions onto farm and/or log out, but not strictly necessary. It is polite because it will help farm deallocate the resources.

You can close sessions by closing the Terminal or MobaXTerm window that you used to connect in.

The more formally correct thing to do is this, in the window where you ran the `srun` and `rserver-form`:
* hit CTRL-C to "cancel" `rserver-farm` and stop the RStudio job.
* type `exit` to exit the srun session

and then you're actually done. But closing the window will essentially accomplish the same, I think.

## 4. General background for working in the UNIX shell

All of the commands we're running at the prompt that looks like this:
```
(base) datalab-02@farm:~$ 
```
are being run at **the UNIX shell**. The "shell" is a layer around all the services that the computer operating system provides, and it lets you ask the computer to do certain things - typically, move files around or execute computational tasks on files.

There are many many many details to learn about using the shell effectively, and we'll cover some of them in Lab 3 and the rest of the course. There are entire books on this, too :) - I recommend Vince Buffalo's "Biological Data Skills" as a good overview!

For now, I would recommend skimming the content and maybe watching videos from the first four workshops from the 2021 Remote Computing training we did at DataLab: [link](https://ngs-docs.github.io/2021-august-remote-computing/).
* Workshop 1: [Introduction to the UNIX Command Line](https://ngs-docs.github.io/2021-august-remote-computing/introduction-to-the-unix-command-line.html) ([video](https://video.ucdavis.edu/media/Intro+to+the+UNIX+Command+Line/1_lcij2vm2))
* Workshop 2: [Creating and modifying text files on remote computers](https://ngs-docs.github.io/2021-august-remote-computing/creating-and-modifying-text-files-on-remote-computers.html) ([video](https://video.ucdavis.edu/media/Creating+and+Modifying+Text+Files+on+Remote+Computers/1_z0lantu4))
* Workshop 3: [Connecting to remote computers with ssh](https://ngs-docs.github.io/2021-august-remote-computing/connecting-to-remote-computers-with-ssh.html) ([video](https://video.ucdavis.edu/media/Connecting+to+Remote+Computers+with+SSH/1_806ws8at))
* Workshop 4: [Running programs on remote computers and retrieving the results](https://ngs-docs.github.io/2021-august-remote-computing/running-programs-on-remote-computers-and-retrieving-the-results.html) ([video](https://video.ucdavis.edu/media/Running+Programs+on+Remote+Computers+and+Retrieving+Results/1_6wvl21uo))

Note that _this_ course (GGG 298 WQ 2023) is going to focus on using RStudio for editing which changes some things (e.g. Workshop 2 is less relevant), but all of the information in the workshops linked above will work just fine whether or not you're using RStudio.