# On the epistomology of Normalization in Single Cell RNAseq
"Normalization" is one of those terms that is heavily overloaded in different fields.
In some fields, it refers to a mechanistic calibration of an instrument based on standards and a well-characterized physical model.
In other fields, it's just some semi-empirical fudge factor that handles factors that we can't model.
In statistics, it is can be thought of a form of conditional inference, and is ubiquitous.
Any time we have a contingency table whose margins are fixed by design or convenience, we should be conditioning on them.
The "normalization" variant of this would be to transform the data, rather than work in the conditional model.
Although there may be some sort of robustness-efficiency tradeoff between using the conditional model and transforming the data, a mathematical purist prefers the conditional model.

## Gene expression fudge factors through the ages
In gene expression analysis, normalization is generally of the semi-empirical fudge-factor variety, and has gone through a variety of epochs.
For microarrays, the arrays themselves had background signal that needed to be accounted for somehow, and it was certainly tempting to just subtract it off the data.
Of course, the amount of cDNA added to the microarray globally affects the signal, and although it subject to imperfect experimental control, it is tempting to subtract or scale the data based on some data-driven estimate of this factor.
In RNAseq analysis, the depth of sequencing is the obvious factor to include, which leads to scaling normalizations such as FPKM and TPM.
The factor factor can also take the form of a pseudo-prior.
If we believe that most genes are not differentially expressed, then then expression should have globally similar quantiles, leading to TMM and many others.

## Can be a way to change the parameter of interest
Absolute vs relative normalizations

## State of single cell normalization
Scaling based.  Spike-in based.  Extremely data driven (D Risso & Co).

## Replication is the answer
Ultimately, normalization is an attempt to manage, in-silico, nuisance experimental variability.
This is a good and proper thing to do, as long as our models are half-way informed.
But never forget: time heals all wounds, and replication heals all unmodeled sources of variability.

>Note that, unlike endogenous mRNA content, which is fixed for a given cell, the remaining effects listed in Box 1 are random (if the same cell could be processed twice, these quantities would vary). This implies that scaling factors are inherently random. Nevertheless, most existing methods treat these scaling factors as fixed factors and/or model offsets.

Random?  But for a given library, there is a true value that can be estimated (subject to error).

>Consequently, by considering all the above factors, we expect to observe nj × Fj × Aj × Dj × Rj reads from cell j.

Which of these are identifiable?  Does it make sense to talk about a single mRNA molecule, given PCA amp and mapping?
