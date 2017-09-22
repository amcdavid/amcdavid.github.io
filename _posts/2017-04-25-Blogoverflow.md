# Blogoverflow: those pesky unix idioms that you keep googling
Mainly relating escaping shell globs, it seems.  Maybe next time I will find my own blog?

### Rsync only files matching the pattern "*.R"
`sh rsync -rv --include="*/" --include="*.R"  --exclude="*"  . bluehive:HurdleNormal/`

### Remove non-printable characters from a text file

`sh perl -i.bak -pe 's/[^[:ascii:]]//g' lecture3-variance-bias-crossvalidation.Rmd`
