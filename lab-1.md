---
tags: ggg, ggg2023, ggg298
---

# Week 1 lab notes - GGG 298 - Jan 11, 2023

[![hackmd-github-sync-badge](https://hackmd.io/XtOHW_gbSwS3zSHgshRupA/badge)](https://hackmd.io/XtOHW_gbSwS3zSHgshRupA)

[toc]

## Today!

Rough plan -

* Introductions!
* How the course will work!
* Labs: background & motivation; some hands on stuff.
* Syllabus overview

## Important news and timely updates!

* no discussion section tomorrow, Jan 12th; first discussion section will be next week.
* _probably_ no lab next Wed, Jan 18th - I scheduled a QE before class time was fixed, my apologies :(. I will update you on Friday and probably provide a recording for you to watch.
* This is a 2-credit course. Many of you have signed up for different numbers of credits. I'll be giving you guidance on fixing this :).

(Please pay attention to Canvas announcements :)

## Syllabus & links

The syllabus is [here](https://hackmd.io/Y3aIAoJsR_y-F-e2_UqZHw?view).

All class materials will be mirrored to GitHub at [ngs-docs/2023-GGG298](https://github.com/ngs-docs/2023-GGG298).

They will remain available indefinitely ;)

## Introductions!

Hello! I'm Titus!

* prof in Vet Med
* research focus is metagenomics specifically and genomics more broadly
* emphasis on data analysis, data reuse, automation, reproducibility, open science, open source, etc. etc.
* also very community focused (open, online)
* Faculty Director of Community Initiatives here at DataLab

I use everything I'll be teaching you here on a daily basis. It's very much _au courant_ in terms of data science and data analysis in bioinformatics.

On a personal level, I'm old but I think not like super old; I have two kids; I like cats and dogs both; I'm an infovore; and I like reading SF&F as well as (recently...) LitRPG.

I blog at http://ivory.idyll.org/blog/ and I tweet at http://twitter.com/ctitusbrown and I mastodon at https://genomic.social/@ctb.

## This course

This course consists of two components - a hands-on lab/practical section (here! today!) and a discussion section where we read something (a paper, or a blog post, or ...) and then discuss it.

Each of you will be involved in introducing a paper! And I will be asking for volunteers for next week. More on that later.

## Let's do something hands on!

I prefer to run computational courses in a hands-on way, because (a) it shows people that stuff really works, (b) it provides space to ask questions, (c) it's practical ;). (And I'm always happy to answer questions about "why this?")

So let's start by doing something hands on!

We're going to run a little workflow to compare 3 microbial genomes and display a similarity matrix and dendrogram.

The workflow source code is [here](https://github.com/ngs-docs/2023-ggg298-sourmash-compare), and you can run it by clicking the badge below:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ngs-docs/2023-ggg298-sourmash-compare/stable?urlpath=rstudio)

This should, in ~30s-2min, create an RStudio Server.

Then go to 'Terminal' and type:

```
snakemake -j 2
```

Things will run! Files will be created! And 

Things to cover:

* the "binder" (See mybinder.org) installs and runs an isolated copy of the GitHub repository (repo) each time you click on that button.
* this binder runs an RStudio Server on a remote Google Cloud computer
* when you run `snakemake -j 2` it is running a data analysis pipeline that does a few things:
    * downloads 3 microbial genomes
    * generates k-mer sketches of each of the genomes using [sourmash](https://sourmash.readthedocs.io/)
    * compares the three genomes
    * builds a comparison matrix and dendrogram! (see file `compare.mat.matrix.png`)
* this pipeline is completely automated in a [snakemake](https://snakemake.readthedocs.io/) workflow, and described in [a Snakefile](https://github.com/ngs-docs/2023-ggg298-sourmash-compare/blob/main/Snakefile)
* you'll notice [the underlying github repository](https://github.com/ngs-docs/2023-ggg298-sourmash-compare) does not have any data or analyses in it! Here, the workflow downloads everything when it runs.
* nor does it include any software - instead, it has a file, [environment.yml](https://github.com/ngs-docs/2023-ggg298-sourmash-compare/blob/main/binder/environment.yml), that describes what software _should be installed_ by [conda](https://docs.conda.io/en/latest/).
* (we'll be learning about snakemake and conda in this class - as well as git/github)

Here's what's being run - this is a workflow diagram automatically produced by snakemake.

![workflow](https://github.com/ngs-docs/2023-ggg298-sourmash-compare/raw/main/doc/workflow-dag.png)

Each oval represents a specific computational action or step.

Q: How many steps are required to analyze three genomes?

Q: How many steps would be needed to analyze four genomes? 5? 6?

(This is a pretty typical style of bioinformatics workflow - and a very simple example :). Most workflows involve many more steps!)

More features:

* this workflow downloads publicly available data automatically! e.g. [the Shewanella baltica OS185 genome](https://www.ncbi.nlm.nih.gov/assembly/GCF_000017325.1/)
* it's easy to rerun from scratch! yay reproducibility and configurability!
* it automatically installs specific versions of software, yay reproducibility!
* it's easy to add samples! yay efficiency!
* it parallelizes easily! yay!
* the files are nicely organized...
* if any step fails, snakemake will let you know clearly and loudly!
* it's easy to send this workflow to others - it's versioned, it's automated, it installs everything for you (yay collaboration! open science! yay reproducibility!)
* you can copy and change the workflow yourself!
* if I update the workflow, both you and I can track how I've changed the workflow!

Even more:

* this repository has a DOI and can be cited! see [the zenodo page](https://zenodo.org/account/settings/github/repository/ngs-docs/2023-ggg298-sourmash-compare); you even get a nifty badge: [![DOI](https://zenodo.org/badge/587375230.svg)](https://zenodo.org/badge/latestdoi/587375230)
* it's actually pretty easy for you to suggest changes to the workflow, too - yay collaboration!
* the binder stuff is cool and builds pretty easily on top of git/github and conda!

### Taking a step back

Everyone doing data science has to do the following:

- managing collections of files
- installing software
- running software with the right arguments and parameters
- running software commands in the right order
- processing and producing visualizations
- using many different languages (here, Python and shell; there, R)

and this workflow is an example of that, just implemented in a particular way. I find it really cool ;).

### Concluding thoughts to the hands-on section

This is a lot of different concepts, I know, and may be pretty overwhelming. That's ok!
We'll step through a lot this stuff this quarter, slowly and carefully.

Importantly, everything above is free and open source, so you can use it, adapt it, etc. yourself.

Part of what I hope to convey to you all is the underlying _mindset_:
* automation is both efficient and good for reproducibility.
* it's just another skill to learn, like pipetting.
* these are broadly useful skills!
* even small steps can be useful! you don't have to instantly switch to being fully automated!

and even if you don't end up using this stuff yourself, today, you should know that it exists!

## Lab section, revisited

So.

Over the next 10 weeks, I'll be showing you a bunch of the skills needed to do this kind of thing on your own.

Right now, I plan to cover:

* UNIX shell and using remote computers (the farm HPC)
* Using conda to install software
* Using git and github to place your data analysis scripts under version control and make them available to others (if you want to)
* Using the snakemake workflow system to automate data analysis pipelines
* Using RStudio Server on farm to edit files and run things; and maybe using Jupyter Notebook to do the same
* RMarkdown 
* Using the slurm queuing system on farm to run long-running analyses

as these are the key building blocks of modern bioinformatics (and data science analyses generally).

What I won't be covering, intentionally:

* how to program in R and/or Python - that's just out of scope for this class, sorry!
* how to analyze a particular type of data / do a particular analysis (although I'll be talking about that in GGG 201(b) on Friday mornings...)
* various kinds of intermediate stuff, although I do plan on running a bunch of ad hoc workshops this quarter as part of DataLab; more on that later.

So, by the end of this course, you'll have hands-on familiarity with UNIX shell, conda, snakemake, git and github, and a few other things. Yay! Yay?

### Concluding thoughts, lab section.

There's no homework.

We'll be hybrid friendly; just let me know if you can't make it for any reason.

I'll record these sessions and the recordings will be available through Canvas.

## Discussion section!

The discussion section is _largely_ decoupled from the lab section.

It's meant to introduce you to interesting (and maybe challenging) questions and concepts. It's pretty free form and you don't need to speak but you are encouraged to do so.

The discussion section is going to be in person only. Sorry. Right now it's scheduled to be in Bainer 1128. I don't know anything about that room tho ;).

There will be weekly readings, with a question to answer.

Even if you can't attend, you should hand in the homework ;).

### First reading and homework question -

Please read [Principles of Data Analysis, Stoudt et al., 2021](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008770).

Question for first reading: what role does hypothesis testing play in data analysis projects, according to Stoudt et al? And/or what is the proportion of time in a project that is to be spent on hypothesis testing (either your opinion or theirs :)?

Please provide your answer in [this form](https://docs.google.com/forms/d/e/1FAIpQLSez0tGahH7_Ook8wDMWRBZ0_paCyoVN4rjMpdpW8x_frMFZvQ/viewform) by 11:59pm on Wednesday, Jan 18th.

### I'm looking for a few good people!

I would like to ask for volunteers - I need four people who will prepare a total of four slides (one per person) -

* brief description of paper (1 slide)
* how the paper relates to the question (I asked (1 slide))
* 2 answers to question (2 slides, one answer per slide)

Slide presentation should take no more than 10 minutes total, and should be viewed as a conversation starter.

Raise hands and/or drop me an e-mail ctbrown@ucdavis.edu if you are up for this!

(Everyone will have to do one, so... might as well get it out of the way?)

If I don't hear back by Friday morning, I'll just pick a few people and e-mail them.

## Let's go through the syllabus together!

Yay fun!

## Reminders

* no class tomorrow
* almost certainly no class next Wednesday
* need 4 volunteers to present next Thursday