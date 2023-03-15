---
tags: ggg, ggg2023, ggg298
---
# Running workflows in multiple languages & using data analysis notebooks - GGG 298 - Week 10, part 2!

Part 1 is [HERE](https://hackmd.io/qlYFV1kPSgClYO0Lvyl7MA?view).

## Running RStudio Server on farm in a custom conda environment

Close out of RStudio server.

Hit CTRL-C to kill `rstudio-launch`.

Now, in the sourmash compare directory, run:

```
cd ~/2023-ggg298-sourmash-compare/
mamba env create -n lab10 -f binder/environment.yml
```

Once that finishes, run:
```
mamba activate lab10
```
and _now_ run
```
module load rstudio-server/2022.12.0
rstudio-launch
```

and reconnect as usual with ssh tunneling etc.

Now "knitting" should work :tada:!



## This also works in binder

Try:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ngs-docs/2023-ggg298-sourmash-compare/stable-rdev?urlpath=rstudio)

Can you run everything there, too?

(It's the same repository, same code, same... everything!)