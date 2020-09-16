# Tri-ROPS
*Trinity RepeatMasker Output Parse Script*

**OUTLINE**

This R script aims to parse RepeatMasker.out files generated from de-novo Trinity data for better tranposable element annotation across whole transcriptome sequences.


The script conducts four key analyses:

1) Removes repetitive elements not classed as TEs (e.g. microsatellites, simple repeats & sRNAs).
2) Merges elements found on the same transcript if they have the same name, oritentation and their combined sequence length is less than or equal to the corresponding reference sequence in RepBase.
3) In cases where multiple copies of the same element are found across different isoforms of the same gene, only one is retained. This ensures that each trasposable element 
4) Merged repeats with a length less than 80bp are removed. 

**USAGE**
The R script is compatible with any output file from RepeatMasker (.out) derived from Trinity based transcriptome sequences. 

Necessary inputs include:
1) RepeatMasker.out file
2) RepeatMasker library used (e.g. RepBase or custom based repeat library) in .fasta format
