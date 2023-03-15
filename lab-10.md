---
tags: ggg, ggg2023, ggg298
---
# Running workflows in multiple languages & using data analysis notebooks - GGG 298 - Week 10!

[![hackmd-github-sync-badge](https://hackmd.io/qlYFV1kPSgClYO0Lvyl7MA/badge)](https://hackmd.io/qlYFV1kPSgClYO0Lvyl7MA)


## Setting things up on farm

We're using slightly different commands today -

So, ssh into farm and do an srun:
```
srun -p high2 --time=3:00:00 --nodes=1 \
    --cpus-per-task 4 --mem 10GB --pty /bin/bash
```

Activate the RStudio server module:
```
module load spack/R/4.1.1
module load rstudio-server/2022.12.0
```

Run `rstudio-launch`:
```
rstudio-launch
```

and follow the instructions to set up your ssh tunneling connection and log in to the RStudio Server.

## Now clone and install the workflow!

Your first mission, should you choose to accept it:

Go to [this repository](https://github.com/ngs-docs/2023-ggg298-sourmash-compare) and click "fork" (upper right).

Once that is completed, you will have a copy in your GitHub account!

Clone _your_ copy of the repository into your farm account and run it.

Questions to be answered:

* what "human-readable" output files are created?
* what code/file creates compare.mat.png?
* what code/file/program creates compare.rstats.png?

Please do the following, in whatever order you like:
* change the color palette for the R script & pheatmap to use the 'inferno' palette;
* change output from png to pdf in R script;
* change output from png to pdf in the sourmash shell;
* add [this genome](https://www.ncbi.nlm.nih.gov/assembly/GCF_026072915.1/) and [this genome](https://www.ncbi.nlm.nih.gov/assembly/GCF_000436395.1/) into the workflow.

Run your new workflow, make sure it all works.

And now commit and push back to your fork.

TODO:
* add a few genomes
