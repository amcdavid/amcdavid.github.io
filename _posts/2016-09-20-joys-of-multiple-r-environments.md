# On the joys of running multiple R environments
Once you have reached a certain level of depravity, it no longer suffices to have a single R environment, where the environment can be defined as the R version, the version of all packages, and possibly the version of the compiler and linear algebra libraries that compiled the whole mess to begin with.
Such perversion arises when you are developing a package and need to develop against R/Bioconductor development, or you need to run a legacy version of R.

Herein find some notes:

1. You can tell R where to look for its package libraries by setting the environment variable `R_LIBS_USER` to a non-default directory, eg, `R_LIBS_USER=~/R/x86_64-unknown-linux-gnu-library/3.3-bioc-release` tells R to put `~/R/x86_64-unknown-linux-gnu-library/3.3-bioc-release` first in the places it looks for packages (the `.libPaths()` search order).
2. Standard advice is to make an alias, ie, in `.bashrc`:

   ```sh
alias R-devel R_LIBS_USER=~/R/x86_64-unknown-linux-gnu-library/3.4-bioc-devel R
   ```
3. But this doesn't work easily or well if you are trying to run R remotely, say via ESS/tramp in emacs.  Instead it is better to write a few shell scripts

   ```sh
#!/bin/bash
#put this in a file called R-devel accessible on your path
R_LIBS_USER=~/R/x86_64-unknown-linux-gnu-library/3.4-bioc-devel R "$@"
   ```
4. This seems not to be entirely respected by `devtools` 1.12.0.  At least when you call `check`, it has complicated ways of mangling the library paths that break this, I believe during the  "checking whether package XXX can be installed" phase.
So you will probably have to call `R-devel CMD check myPackage.tar.gz` from the shell.
Details currently under investigation.
5. It's possible that using [packrat](https://cran.r-project.org/package=packrat) might obviate the custom `.libPaths()` situation, but not the multiple versions of R situation.
But I haven't had great luck with packrat (probably my own fault).

## 2017.01.04 Addendum
Working multiple R versions via [ESS/TRAMP](https://www.gnu.org/software/emacs/manual/html_node/tramp/index.html#Top) requires even more bizarre incantations.
Supposedly, ESS is supposed to discover R versions searching the EMACS variable `exec-path` for commands starting with strings provided in the list `ess-r-versions`, though even this doesn't seem to work on MacOS.
It definitely doesn't simply work with TRAMP, which sets its own remote PATH based on the variable `tramp-remote-path`.
This, in turn, takes default values that generally don't reflect the PATH you'd get with a standard login shell on the remote system.
Instead, to find a version of R, you may alter `tramp-remote-path` to put the directory containing your desired version first in the path list, eg, with `M-x customize-variables tramp-remote-path`.

