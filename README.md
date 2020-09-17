# RM_TRIPS
*RepeatMasker Trinity based Parse Script*

Author = Chrstopher L Butler

Email = c.butler@uea.ac.uk

**OUTLINE**

This R script aims to parse RepeatMasker.out files generated from de-novo Trinity data for better transposable element (TE) annotation across whole transcriptome sequences. Output is given in .CSV format, in order for further analysis to be conducted at ease. 


The script conducts four key steps:

1) Repetitive elements not classed as TEs (e.g. microsatellites, simple repeats & sRNAs) are removed.
2) TEs found on the same transcript are merged if they have the same element name, orientation and their combined sequence length is less than or equal to the  corresponding reference sequence in RepBase.
3) In cases where multiple copies of the same element are found across different isoforms of the same gene, only one is retained. This ensures that each trasposable element corresponds to a unique genomic loci. 
4) Merged repeats with a length less than 80bp are removed. 


**USAGE**

The R script is compatible with any output file from RepeatMasker (.out) derived from Trinity based transcriptome sequences. 

Necessary inputs include:
1) The RepeatMasker.out file
2) The RepeatMasker library used (e.g. RepBase or custom based repeat library) in .fasta format

The output is given as a .csv file and is written in the directory in which the .out file is found.

*Note*

Before running RM_TRIPS, you may want to ensure that your RepeatMasker.out file only contains distinct repeats by removing repeats which have a lower scoring match whose domain partly includes the domain of the current match, as indicated by an asterisk * in the final output column. 

This can be achieved by running the following bash shell script -

```
awk '!/\*/' $file.out > noasterisk$file.out
```

![Visual Depiction of Four Key Steps Conducted by RM_TRIPS]<src="https://user-images.githubusercontent.com/71394626/93374909-4d3a6980-f84f-11ea-8f52-7378f976cd75.png">


<img align="right" width="100" height="100" src="https://user-images.githubusercontent.com/71394626/93374909-4d3a6980-f84f-11ea-8f52-7378f976cd75.png"
