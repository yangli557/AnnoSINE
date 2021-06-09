# Table of Contents
- [Introduction](#heading)
- [Installation](#heading-1)
  * [Sub-heading](#sub-heading-1)
    + [Sub-sub-heading](#sub-sub-heading-1)
- [Inputs](#heading-2)
- [Outputs](#heading-3)
- [Usage](#heading-4)
- [Citations](#heading-2)

# Introduction
AnnoSINE program (in Python) is designed to generate high-quality non-redundant SINE libraries for genome annotation. It uses the manually curated SINE library in the *Oryza sativa* genome to benchmark the annotation performance.

AnnoSINE has eight major modules. The first one is to identify putative SINE candidates by applying hidden Markov model (HMM)-based homology search or structure-based *de novo* search. This step is usually sensitive but can output many false SINE candidates. Second, we search for target site duplication (TSD) in the flanking region to further verify each SINE candidate. As TSD is a significant feature of SINEs, this step is highly effective in removing non-SINEs. Although searching for TSD can be conducted in the later stage of the pipeline, removing false positives earlier can save the computational time of the downstream analysis. In the 3rd step, we examine the copy number and the alignment of SINE copies to remove the sequences with few copy numbers or shifted/fragmented alignments. In addition, we can identify some lineage-specific differences, such as the length of the 3' end using the alignment profile. In the 4th step, we decide the superfamily of each candidate SINE sequence and remove highly similar candidates from known non-coding RNAs. Meanwhile, the highly identical sequences assembling to RNA are false positives. In the 5th step, we remove candidates with a large proportion of tandem repeats. In the 6th step, we remove other TEs by detecting inverted repeats adjacent to TSDs. These steps focused on identifying complete SINEs (i.e., *seed sequences*) in the query genome. Redundant seeds are filtered to generate the SINE library. After we obtain the non-redundant seed sequences, we will apply RepeatMasker to identify other SINEs to complete the whole genome SINE annotation in the last step.

# Installation
AnnoSINE is developed in Python with dependences: HMMER, TSD Search, BLAST, TRF, IRF, CD-HIT, RepeatMasker
