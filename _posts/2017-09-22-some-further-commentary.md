# Some further commentary on proper hygene of the R library search path (especially w/r/t MacOS)

## TL;DR
Only put stable, universal packages in the default R system library (`/Library/Frameworks/R.framework/Resources/library`).  Write protect it to enforce this policy.

## Long version:
1. By default, not-root has write permissions to the default R system library
2. There's no way to remove  the default R system library from R's search path, that I can tell, on Mac OS.
3. If a package is present at the default R system library, `biocLite` will try to update and over-write the package at this location, rather than adding a new version at`R_LIBS_USER`.  Hence ignoring the search order in `.libPaths()` and argument `lib.loc`. 
4. Therefore, to avoid unintentionally altering your configuration, change the permissions of the R system library so that you can't casually write there (eg with `sudo chmod -R 755 /Library/Frameworks/R.framework/Resources/library`)
5. Now, however, if a package is present in the now write-protected site library, `biocLite` and `install.packages` will moan and die about a lack of permissions, rather than falling back (well, actually forward) to a write-able, higher-order location in `.libPaths()`.
6. Therefore, move all packages that you might have to manage on a per-project basis to a separate, user-writable folder, and set this as R_LIBS_USER in your .Renviron file.
7. Now you may override or add to this value on a per-project basis.
