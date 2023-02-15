---
tags: ggg298, ggg2023, ggg
---
# Practice Makes Perfect (with shell, conda, and snakemake) - GGG 298 winter 2023, week 6

[toc]

TODO:
* post about plans
* set up hackmds
* push to github?

([Permanent link](https://github.com/ngs-docs/2023-GGG298/blob/main/lab-6.md))

## organization

online breakout room

in person groups - ask people to sit together

quick tutorial on using hackmd

### Using hackmd

I've set up 6 hackmds with edit privileges for everyone. I'll show you a few tricks to using them; here are some notes!

* you can switch between edit and view mode in upper left
* Use a region in the editor bounded by `~~~` on either side (at beginning of line) to paste code examples
* use `*` at the beginning of a line to start a bullet list
* use `#` or `##` at the beginning of a line to start a new title

## Instructions

Do all of the below in your farm account. You should use RStudio unless you prefer to use something else.

### Account preparations - download data

Make sure you have the `~/data` subdirectory in your account:
```
cd ~/
wget https://s3-us-west-1.amazonaws.com/dib-training.ucdavis.edu/shell-data.zip
unzip -u shell-data.zip
```

### TASK 1: using multiple working directories


Record (in the hackmd) the commands you run to do the following:

Change your current working directory to be the path:
```
~/data/MiSeq
```

List the files in the directory `~/data/.hidden` using a _relative_ path, i.e. using a path starting with `..` rather than a path starting with `/`.

Change your current working directory  to be `~/data/.hidden/tmp1`, using a relative path.

List the files in the directory `~/MiSeq` using a relative path.

Victory conditions:
* list all of the commands you used in the hackmd.

### TASK 2: installing software with conda/mamba

Links:
- [conda lesson from week 4](https://hackmd.io/VTcCz9dmSf6vclaHRwavlw?view)
- [tree man page](https://linux.die.net/man/1/tree)

Create a new conda environment with the `tree` program installed.

Run `tree -ad ~/data`.

Victory condition:
* put the mamba commands used to create/install/activate tree in the hackmd.
* use mamba to find the version of tree that was installed and put it in the hackmd.
* paste the output of running `tree` on `~/data` in the hackmd.

### TASK 3: downgrade the version of `tree`

Use `mamba search` to find the available versions of tree.

Then use `mamba install` to downgrade the version of tree in your conda environment to a n older version.

Finally, use `mamba list` to show the version of tree that is installed.

Victory condition:
* put the mamba commands for `search`, `install`, and `list` (that you used above) in the hackmd.

### TASK 4: Use snakemake to compress some files

Links:
* [week 4 snakemake lesson](https://hackmd.io/kkosFQV5RhiMAzKNFxA2Mw)
* [snakemake book chapter 6: intro wildcards](https://ngs-docs.github.io/2023-snakemake-book-draft/chapter_6.html)
* [snakemake book chapter on more wildcards](https://ngs-docs.github.io/2023-snakemake-book-draft/beginner+/wildcards.html)

In the `~/data/MiSeq` directory, create a Snakefile that uses gzip to compress four or more of the `.fastq` files in this directory.

You can start with this Snakefile:
```
rule all:
    input:
        "F3D141_S207_L001_R1_001.fastq.gz"
        
rule compress:
    shell:
        "gzip -k {input}"
```

Victory conditions:
* paste the entire Snakefile contents into the hackmd.
* please include the command you're using to run snakemake!

### TASK 5: use snakemake to run fastqc on four or more fastq.gz files.

Create a mamba environment containing fastqc and snakemake-minimal.

Create a Snakefile in the `~/data` directory (NOT in the `MiSeq` subdirectory) that runs fastqc on four or more of the fastq.gz files.

Victory conditions:
* paste the mamba commands into the hackmd.
* paste the entire Snakefile contents into the hackmd.
* please include the command you're using to run snakemake!

### TASK 6: use snakemake to run multiqc on the `~/data/MiSeq` directory.

Install the `multiqc` program and adjust the Snakefile created previously to run multiqc.

You should run `multiqc` in the `data` directory like so:
```
multiqc .
```

(You can see some example output [here!](https://farm.cse.ucdavis.edu/~datalab-02/2023-ggg298-week6/multiqc_report.html))

Hint: you'll need to determine what the output files are for yourself! One of them is a directory and you'll need to use `directory('name')` instead of just `'name'` in the `output:` block.

Verify that the following commands delete all the output files and then rerun everything from scratch:
```
snakemake -j 1 --delete-all-output
snakemake -j 1
```

Victory conditions:
* paste the mamba commands into the hackmd.
* paste the entire Snakefile contents in to the hackmd.
* please include the command you're using to run snakemake!

**ADVANCED:** run the following to make your multqic reports available from outside farm:
```
chmod a+x ~/
mkdir -p ~/public_html/lab6/
cp -r multiqc* ~/public_html/lab6/
```
and then your multiqc report should be available at `https://farm.cse.ucdavis.edu/~datalab-XX/lab6/multiqc_report.html`

### TASK 7: (advanced) Use glob_wildcards to automatically compress the remaining .fastq files.

Create a _new_ Snakefile named `Snakefile.glob` in `~/data`.

At the top of this Snakefile, use the following to retrieve and then work on a list of all .fastq.gz files under the data directory:

```
FASTQ_FILES, = glob_wildcards('{f}.fastq')

rule all:
    input:
        expand('{f}.fastq.gz', f=FASTQ_FILES)
```

Fill in the rest of the file from your above work with gzip, so that the Snakefile compresses all the remaining .fastq.gz files.

Remember: to run snakemake using Snakefile.glob, you will need to specify the name of the snakefile to use with `-s <filename>`.

Victory conditions:
* paste the entire Snakefile contents in to the hackmd.
* please include the command you're using to run snakemake!

### TASK 8: (advanced) Add glob_wildcards into your `~/data/Snakefile` snakefile so that FastQC/MultiQC is run on all the files.

Victory conditions:
* paste the entire Snakefile contents in to the hackmd.
* please include the command you're using to run snakemake!

### TASK 9: (advanced) Combine Snakefile and Snakefile.glob into one Snakefile

Make it so that running this in the `~/data` directory gzips all the files and runs FastQC and MultiQC on them.
```
snakemake -j 1 --delete-all-output
snakemake -j 1
```

Victory conditions:
* paste the entire Snakefile contents in to the hackmd.
* please include the command you're using to run snakemake!
