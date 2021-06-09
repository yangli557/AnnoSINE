# AnnoSINE

SINE Annotation Tool for Plant Genomes

# Table of Contents
- [Introduction](#heading)
- [Installation](#heading-1)
  * [Sub-heading](#sub-heading-1)
    + [Sub-sub-heading](#sub-sub-heading-1)
- [Testing](#heading-2)
- [Inputs](#heading-2)
- [Outputs](#heading-3)
- [Usage](#heading-4)
- [Citations](#heading-2)

# Introduction
AnnoSINE program is designed to generate high-quality non-redundant SINE libraries for genome annotation. It uses the manually curated SINE library in the *Oryza sativa* genome to benchmark the annotation performance.

AnnoSINE has eight major modules. The first one is to identify putative SINE candidates by applying hidden Markov model (HMM)-based homology search, structure-based *de novo* search or combinition of homology-structure-based search. This step is usually sensitive but can output many false SINE candidates. In the 2nd step, it searches for target site duplication (TSD) in the flanking region to further verify each SINE candidate. As TSD is a significant feature of SINEs, this step is highly effective in removing non-SINEs. Although searching for TSD can be conducted in the later stage of the pipeline, removing false positives earlier can save the computational time of the downstream analysis. In the 3rd step, it examines the copy number and the alignment of SINE copies to remove the sequences with few copy numbers or shifted/fragmented alignments. In addition, it can identify some lineage-specific differences, such as the length of the 3' end using the alignment profile. In the 4th step, it decides the superfamily of each candidate SINE sequence and remove highly similar candidates from known non-coding RNAs. Meanwhile, the highly identical sequences assembling to RNA are false positives. In the 5th step, it removes candidates with a large proportion of tandem repeats. In the 6th step, it removes other TEs by detecting inverted repeats adjacent to TSDs. These steps focused on identifying complete SINEs (i.e., *seed sequences*) in the query genome. Redundant seeds are filtered to generate the SINE library. After we obtain the non-redundant seed sequences, it will apply RepeatMasker to identify other SINEs to complete the whole genome SINE annotation in the last step.

# Prerequisites
To use AnnoSINE, you need to install the tools listed below.

 - [Python &emsp; &nbsp; &emsp; 3.7.4](https://www.python.org/)
 - [HMMER &emsp; &emsp; &emsp; 3.3.1](http://hmmer.org/download.html)
 - [BLAST+ &emsp; &nbsp; &ensp; 2.10.1](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.10.1/)
 - [TRF&emsp;&emsp;&ensp;4.09](https://tandem.bu.edu/trf/trf.download.html)
 - [IRF&emsp;&emsp;&ensp;3.07](https://tandem.bu.edu/irf/irf.download.html)
 - [CD-HIT](http://weizhongli-lab.org/cd-hit/download.php)
 - [RepeatMasker 4.1.2](http://www.repeatmasker.org/RepeatMasker/)

# Usage

```
python AnnoSINE.py [options] <mode> <input_filename> <output_filename>
```

## Argument Description
```
positional arguments:
  mode                  [1 | 2 | 3]
                        Choose the running mode of the program.
                                1--Homology-based method;
                                2--Structure-based method;
                                3--Hybrid of homology-based and structure-based method.
  input_filename        input genome assembly path
  output_filename       output files path

optional arguments:
  -h, --help                 show this help message and exit
  -evalue1, --hmmer_evalue   Expectation value threshold for saving hits of homology search (default: 1e-10)
  -evalue2, --blast_evalue   Expectation value threshold for sequences alignment search (default: 1e-10)
  -l, --length_factor        Threshold of the local alignment length relative to the the BLAST query length (default: 0.3)
  -c, --copy_number_factor   Threshold of the copy number that determines the SINE boundary (default: 0.15)
  -s, --shift                Maximum threshold of the boundary shift (default: 80)
  -g, --gap                  Maximum threshold of the trancated gap (default: 10)
  -minc, --copy_number       Minimum threshold of the copy number for each element (default: 3)
  -maxb, --base_copy_number  Maximum threshold of copy number for the first and last base (default: 1)
  -p, --probability          Minimum of the length proportion of tandem repeat to element (default: 0.5)
  -b, --boundary             Output SINE seed boundaries based on TSD or MSA (default: tsd)
  -m, --model                Choose the rule/learning mode of repeat pattern examination (default: rule)
```

## Inputs
Genome sequence(fasta format).

## Outputs


# Example:
```
python3 AnnoSINE.py 2 ../Input_Files/GCA_000001735.2_TAIR10.1_genomic.fasta ../Output_Files
```

# Citations
