# RM_TRIPS
*RepeatMasker Trinity based Parse Script*

Author = Christopher L Butler

Email = c.butler@uea.ac.uk


**OUTLINE**

This R script aims to parse RepeatMasker.out files generated from de-novo Trinity data for better transposable element (TE) annotation across whole transcriptome sequences. Output is given in .CSV format so further analyses can be conducted at ease. 


The script conducts four key steps:

1) Repetitive elements not classed as TEs (e.g. microsatellites, simple repeats & sRNAs) are removed.
2) TEs found on the same transcript are merged if they have the same element name, orientation and their combined sequence length is less than or equal to the  corresponding reference sequence in the focal TE library.
3) In cases where multiple copies of the same element are found across different transcript isoforms, only one is retained. This ensures that each trasposable element corresponds to a unique genomic loci. 
4) Merged repeats with a length less than 80bp are removed. 

<p align="center">
<img src="https://user-images.githubusercontent.com/71394626/93374909-4d3a6980-f84f-11ea-8f52-7378f976cd75.png" width="200" height="400" />
</p>


**USAGE**

The R script is compatible with any output file from RepeatMasker (.out) derived from Trinity based transcriptome sequences. 

Necessary inputs include:
1) The RepeatMasker.out file
2) The RepeatMasker library used (e.g. RepBase or custom based repeat library) in .fasta format

The output is given as a .csv file and is written in the same directory where the .out file is found.

| Column Header    | Description                                                    |
|------------------|----------------------------------------------------------------|
| repeat_id        | Name of TE with the significant hit                            |
| qry_id           | Name of Trinity transcript with TE hit                         |
| matching_repeat  | Is match complement (C) of the TE sequence?                    |
| matching_class   | The transposon class in which the TE belongs to                |
| reference_length | Sequence length of the TE as found in the reference library    |
| merged_qrystart  | Start of TE hit found on the transcript                        |
| merged_qryend    | End of TE hit found on transcript                              |
| mergedfraglength | Sequence length of TE hit (bp)                                 |
| perc_div         | % of substitutions in matching region compared to the consesus |
| perc_del         | % of bases opposite a gap in the query sequence                |
| perc_insert      | % of bases opposite a gap in the repeat sequence               |
| Gene             | Gene name                                                      |
| Isoform          | Isoform number                                                 |


*Note*

Before running RM_TRIPS, you may wish to ensure that your RepeatMasker.out file only contains distinct repeats by removing repeats which have a lower scoring match whose domain partly includes the domain of the current match, as indicated by an asterisk * in the final output column. 

This can be achieved by running the following bash shell script -

```
awk '!/\*/' $file.out > noasterisk$file.out
```

Below is a table which details the impact each stage of the parse script has on estimated TE abundance. In this instance _(Corydoras maculifer)_, running RM_trips on a RepeatMasker output against a _Danio rerio_ TE library halves the estimated TE abundance, decreasing from 3.58%  to 1.17%.

<img width="1006" alt="RMtrips_breakdown" src="https://user-images.githubusercontent.com/71394626/132558214-d2f7ecd9-17c1-45d8-bea2-244d9490b0e7.png">





