---
tags: ggg, ggg2023, ggg298
---

# Syllabus for Tools for Data Intensive Research, GGG 298, WQ 2022-2023

[![hackmd-github-sync-badge](https://hackmd.io/Y3aIAoJsR_y-F-e2_UqZHw/badge)](https://hackmd.io/Y3aIAoJsR_y-F-e2_UqZHw)

[toc]


Winter Quarter, 2022-2023
GGG 298 section 88
2 credits (lab + discussion)

Instructor: Titus Brown, ctbrown@ucdavis.edu

WHERE/WHEN: 
* Lab: Wed **12:30-3pm**, Shields 360 (DataLab)
* Discussion: Thursday 1:10-2pm, Bainer 1128

The lab section of this class will be hybrid friendly; please contact Dr. Brown if you need the zoom link for any reason.

(Note that class starts at 12:30pm on Wednesday, not at 12:10; the registrar does not appear to allow nontraditional start times ;).

See bottom of this document for CRN and PTA information.

## Class description

Tools for Data Intensive Research teaches a set of tools for working on remote computing systems with large amounts of data and long-running processes - UNIX shell, snakemake, git/github, conda, R and RMarkdown, etc. The  focus is on bioinformatics use cases, but I do not spend too much time talking about biology and rather focus on how to work with the tools. 

The course is two credits, and consists of one 2.5 hour computational lab and a single 1 hour discussion section per week; weekly homework involves reading that week's paper, answering a question, and (for one of the weeks) doing a small-group mini-presentation on the paper & your answers to the question.

Past attendees have told me that both parts of the course are interesting and that the papers and discussion section is particularly so ;).

The course will be S/U because it is a temporary course. However, in the past some students have been able to get an exception in order to satisfy an elective requirement. Please let Titus know if you need additional information to do so.

## Course description

Here's the course description from the syllabus:

This course will provide a practical introduction to common tools used in data-intensive research, including the UNIX shell, version control with git, RMarkdown, JupyterLab, and workflows with snakemake. The associated discussion section will connect the lab practicals to foundational concepts in data science, including repeatability/reproducibility, statistics, and publication ethics.

This course is open to all graduate students. No prior computational experience is required or assumed. There will be some minimal overlap with GGG 201(b) topics. All materials will be open to the community and freely available online.

## Code of Conduct

Please abide by [my lab's Code of Conduct](http://ivory.idyll.org/lab/coc.html) in this course.

In particular, this is not an intellectual contest, and please realize that we _all_ have plenty of things to learn.

## Homework

There will be 9 paragraph-length homeworks due, one each week on the reading; they'll be assigned a week in advance and due on Thursday at midnight.

Each week several (4-6) students will be asked to take a lead in preparing for the paper discussion on Fridays. Each student will only be asked to do this once.

## Grading

The course is S/U, and only graded on homework; you need to hand in 7 of the 9 homeworks to pass.

## Office hours

Office hours will be by arrangement, and will typically be remote.

Please sign up here in advance: https://calendly.com/ctitusbrown/30min?back=1&month=2022-01, or if nothing is available, please contact Titus via e-mail at ctbrown@ucdavis.edu. The calendly link will provide zoom rooms.

## Attendance and recordings

Lab sessions (on Wednesday) will be broadcast on zoom, as well as recorded. The recordings will be saved for a month, in Canvas. Please ask if you can't find one!

Discussion sessions (on Thursday) will not be broadcast or recorded.

Attendance is expected for both Wednesday and Friday. Please let Dr. Brown know if you can't attend, at ctbrown@ucdavis.edu.

Wed class will be hybrid friendly and you can attend remotely. Ask Dr. Brown for a zoom link.

## In-class chat via Slack

We'll use Slack for sharing links and commands on both days. Please visit ucdavis.slack.com to create an account, and then join the slack channel `#2023-ggg298`.

## Lab topics

Wednesdays, 12:30-3pm.

These will be lab practicals where we take a solid look at a given piece of technology and work through using it together.

### Links to lab notes

1. [Lab 1 - getting started, running workflow once](https://hackmd.io/XtOHW_gbSwS3zSHgshRupA?view)
2. [Lab 2 - logging into farm; RStudio; and running the workflow again](https://hackmd.io/n7_pXRiiRQ-YpQBQ93uW9Q?view)
3. [Lab 3 - farm; multiuser systems; UNIX shell](https://hackmd.io/4Tm5i97QT5iDlZL-IC7U8A?view)
4. [Lab 4 - Installing software on remote computers with conda/mamba](https://hackmd.io/VTcCz9dmSf6vclaHRwavlw?view)
5. Lab 5 - snakemake for workflows
6. Lab 6 - hands-on practice time with conda and snakemake!
7. Lab 7 - Git & GitHub
8. Lab 8 - Shell scripting, parallelization, file organization, and/or slurm for HPC.
9. Lab 9 - remote computing? scripting in R? R/RMarkdown? file organization?
10. Lab 10 - more hands on! Anatomy of a project.

## Paper discussions

Thursday, 1:10-2pm.

These will be discussion periods where we explore the concepts and questions introduced by various papers, articles, and blog posts. The topics will be relevant to data science and the practice of science.

### Week 2 - data science and workflows

Please read Principles of Data Analysis, Stoudt et al., 2021

Question for first reading: what role does hypothesis testing play in data analysis projects, according to Stoudt et al? And/or what is the proportion of time in a project that is to be spent on hypothesis testing (either your opinion or theirs :)?

Please provide your answer by 11:59pm on Wednesday, Jan 18th.

### Week 3 - reproducibility in science

Our next paper is Trust but Verify: How to Leverage Policies, Workflows, and Infrastructure to Ensure Computational Reproducibility in Publication (https://hdsr.mitpress.mit.edu/pub/f0obb31j/release/3, by Willis and Stodden.


Please answer the following question by midnight on Wed, January 25th: **Who decides if a paper is sufficiently reproducible?**

In class on Wednesay we may discuss this question as well: **How do you think "transparency" (as defined in the paper) differs for the experimental and the computational components of biology research? (and what are the implications for reproducibility and/or replicability)?**

### Week 4 - reproducibility in practice

Draft blog post: I found a sizeable bug in our published software. Now what?

https://hackmd.io/@ctb/HJNK-2yk_

Question for third reading: Who should have found this bug, and how would that have worked (e.g. authors, reviewers, journal editors, random Internet people, senior authors’ mothers, etc)? Feel free to refer back to your answer from last week ;).

### Week 5 - reproducibility and correctness in biology

Skim one or both of:
* [5-HTTLPR: a pointed review](https://slatestarcodex.com/2019/05/07/5-httlpr-a-pointed-review/)
* [Functionally Enigmatic Genes: A Case Study of the Brain Ignorome](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0088889)

and then answer the following question:

What's a way forward?

Please specify which study/paper you're addressing ;).

### Week 6 - preregistration

please read EITHER [The preregistration revolution](https://www.pnas.org/content/115/11/2600) OR [Prediction, pre-specification, and transparency](https://featuredcontent.psychonomic.org/prediction-pre-specification-and-transparency/), and then answer the following question:

What good practices does preregistration support, what good practices does preregistration prevent, and/or what bad practices does preregistration encourage, drawing from your own personal experience and/or preconceptions?

(Yes, you can read both papers if you like. :)

### Week 7 - chatgpt and AI

Read two or more of the following articles:

* [A publishing infrastructure for AI-assisted academic authoring](https://www.biorxiv.org/content/10.1101/2023.01.21.525030v1), Pividori and Greene;
* [What would Plato say about ChatGPT?](https://www.nytimes.com/2022/12/15/opinion/chatgpt-education-ai-technology.html), Zeynep Tufekci;
* [Against automated plagiarism](https://irisvanrooijcogsci.com/2022/12/29/against-automated-plagiarism/), 	
Iris van Rooij;
* [The end of organizing](https://every.to/chain-of-thought/the-end-of-organizing)

and then answer the following question:

What, in your opinion, is an ethical use of AI in your scientific work (if any)? Please explore an actual specific use in two or three sentences.

### Week 8 - chatgpt and AI

Skim two or more of the following articles -

* [Human Fallback](https://www.nplusonemag.com/issue-44/essays/human_fallback/) - note, LONG.
* [AI-powered Bing Chat loses its mind when fed Ars Technica article](https://arstechnica.com/information-technology/2023/02/ai-powered-bing-chat-loses-its-mind-when-fed-ars-technica-article/)
* [AI Alignment: getting AIs to do what you want is hard, maybe](https://ai-alignment.com/ai-alignment-is-distinct-from-its-near-term-applications-81300500ad2e)
* [Generative AI: autocomplete for everything](https://noahpinion.substack.com/p/generative-ai-autocomplete-for-everything?ref=weekly-filet)
* [CNET Is Reviewing the Accuracy of All Its AI-Written Articles After Multiple Major Corrections](https://gizmodo.com/cnet-ai-chatgpt-news-robot-1849996151)

and answer this question: based on these articles and our discussion last week, where do you see AI fitting into your actual scientific workflow? What is responsible use vs irresponsible use?

### Week 9 - the impossibility of AI.

Please read [The Impossibility of Automating Ambiguity](https://direct.mit.edu/artl/article-abstract/27/1/44/101872/The-Impossibility-of-Automating-Ambiguity) by Abeba Birhane, as well as [Hundreds of AI tools have been built to catch covid. None of them helped](https://www.technologyreview.com/2021/07/30/1030329/machine-learning-ai-failed-covid-hospital-diagnosis-pandemic/). Then answer the following question:

How many of the failed attempts to predict COVID were due to the kind of conceptual problem that Dr. Birhane poses, vs more mundane interdisciplinary failures to understand the data, vs simple failures to do good science?

### Week 10 - data feminism: bring back the bodies

Please read [Bring back the bodies](https://mitpressonpubpub.mitpress.mit.edu/pub/zrlj0jqb/release/6) by D'Ignazio and Klein.

What are ways of working equitably with data from human bodies, or biology research on animals or resources indigenous to historically/economically marginized countries, or other bio-centric data? What are some costs and concerns of _not_ considering equity that are relevant to your research interests? You can be as broad or narrow as you want.

## Questions and Answers

### Q: The course is currently S/U, but I need it to be graded so it can satisfy an elective in my graduate program. Help!

Unfortunately GGG 298 is a "temporary" course and cannot be turned into a graded course.

If you need it to satisfy an elective, you can request an exception; these have been granted in previous years and I am happy to provide supporting material and arguments as needed.

### Q: Can I audit the course?

Yes! You may attend just the lab, or the lab and the discussion section, or just the discussion section. Just e-mail me to be added to the canvas group.

If you audit, I expect you to attend all sessions, however - e.g. all labs, or all discussions. Thanks!

### Q: Is this course in-person or hybrid?

I'd like to request that most people attend the course in person; please do mask as well.

We will be hybrid friendly. If you need to attend remotely for one or more sessions due to illness or travel, that is fine!

If you need to attend completely remotely, I am more than happy to accomodate this! Please contact me to arrange it.

### Q: Should I take this, or GGG 201(b), or both?

GGG 201(b) is Introduction to Bioinformatics. It is a required course for IGG students.

I teach both GGG 298 (this course) and the lab section for GGG 201(b). Students sometimes want to know which they should take; read on for my answer!

The 201(b) lectures focus on genome and transcriptome sequencing and genomic interpretation, with an emphasis on large genomes; they do not cover microbial genomes or microbiome topics. In 2022-2023, the lectures are given by Prof. Megan Dennis, Dr. Tamer Mansour, and Dr. Daniela Soto.

The labs are taught by me, and focus on  workflows for (1) bacterial genome variant calling, (2) de novo genome assembly, and (3) RNAseq differential expression analysis. The data sets are all microbial because the data sets are small enough to work with the interactively, but the principles generalize to human and plant domains.

You are welcome to audit 201(b) lab only, although I request that you attend all classes and submit all homeworks.

Taking them together is not a bad idea, although you will get a very concentrated dose of me if you do so ;).

There is a lot of shallow overlap between the two classes, but the in depth topics are quite different. GGG 201(b) is much more biologically focused, while GGG 298 is much more about the tooling.

If you can only take one, I suggest taking/auditing GGG 201(b) _before_ taking GGG 298. GGG 201(b) motivates GGG 298, while GGG 298 is a much lighter-weight class with minimal homework, and it might fit better into a second- or third-year research schedule because of that.

### Q: How do I add this course?

The CRN is 27206.

You may need a "permission to add" (PTA) number. If so, please e-mail your student ID number to Najwa Marrush, nmmarrush@ucdavis.edu, asking for a PTA number to enroll in GGG 298 section 5.

### Q: Where the heck is Shields 360?

Shields 360 is the DataLab classroom.

It is not easy to find the first time! So plan to take a few extra minutes to get there!

You can find it by going into the Shields Library, then climbing up the two flights of stairs and going to the right (or taking an elevator up to the 3rd floor). It is all the way in the back of the library on the 3rd floor, in the southeast corner. You should see a big "DataLab" sign on the wall in front of you as you walk back from the stairs in front.
