#         3DAROC

![](/Documents/Logo/Foto-DNA_MMarti_0.jpg?raw=True)


## Course description

3C-based methods, such as Hi-C, produce a huge amount of raw data as pairs of DNA reads that are in close spatial proximity in the cell nucleus. Overall, those interaction matrices have been used to study how the genome folds within the nucleus, which is one of the most fascinating problems in modern biology. The rigorous analysis of those paired-reads using computational tools has been essential to fully exploit the experimental technique, and to study how the genome is folded in the space. Currently, there is a clear expansion on the wealth of data on genome structure with the availability of many datasets of Hi-C experiments down to 1Kb resolution (see for example: http://hic.umassmed.edu/welcome/welcome.php ; http://promoter.bx.psu.edu/hi-c/view.php or http://www.aidenlab.org/data.html ). In this course, participants will learn to use TADbit, a software designed and developed to manage all dimensionalities of the Hi-C data:

 - 1D - Map paired-end sequences to generate Hi-C interaction matrices
 - 2D - Normalize matrices and identify constitutive domains (TADs, compartments)
 - 3D - Generate populations of structures which satisfy the Hi-C interaction matrices
 - 4D - Compare samples at different time points

Participants can bring- specific biological questions and/or their own 3C-based data to analyze during the course. At the end of the course, participants will be familiar with the TADbit software and will be able to fully analyze Hi-C data. Note: Although the TADbit software is central in this course, alternative software will be discussed for each part of the analysis.

## Target Audience

The course design is oriented towards experimental researchers and bioinformaticians at the graduate and post-graduate levels. The last edition of this course was attended by people with different backgrounds and interested in the genome organization.
Moreover, Hi-C data have recently been used in metagenomics studies to accurately cluster metagenome assembly contigs into groups that contain nearly complete genomes of each species.
It is likely that the participants to this course aim at getting involved in generating Hi-C data for chromosome structure determination or that they just want to be able to correctly interpret and analyse publicly available data. 

## Course Pre-requisites

Recommended Linux and basic Python programming skills, graduate level in Life Sciences. 

## Content

|       | Core pipeline | Annex | 
|-------|-----------------|------------|
| day 1 | <ul><li>[Hi-C Quality check](/Notebooks/00-Hi-C quality check.ipynb)</li><li>[Mapping](/Notebooks/01-Mapping.ipynb)</li><li>[Parsing mapped reads](/Notebooks/02-Parsing mapped reads.ipynb)</li></ul> | <ul><li>[Software installation](/Notebooks/A0-Preparing your computer for HiC data analysis.ipynb)</li><li>[Prepare reference genome](/Notebooks/A1-Preparation reference genome.ipynb)</li><li>[Download Hi-C experiment](/Notebooks/A2-Download published Hi-C experiments.ipynb)</li></ul> |
| day 2 | <ul><li>[Filterind reads](/Notebooks/03-Filtering mapped reads.ipynb)</li><li>[Normalization](Notebooks/04-Bin-filtering and normalization.ipynb)</li></ul> | <ul><li>[Compare/merge experiments](/Notebooks/A3-Compare and merge Hi-C experiments.ipynb)</li></ul> |
| day 3 | <ul><li>[Compartments and TADs](/Notebooks/05-Compartments and TADs.ipynb)</li></ul> | <ul><li>[Align and compare TADs](/Notebooks/A4-Align and compare TADs.ipynb)</li></ul> |
| day 4 | <ul><li>[Parameter optimization](/Notebooks/06a-Modeling - parameter optimization.ipynb)</li><li>[Model optimization](/Notebooks/06b-Modeling - model optimization.ipynb)</li></ul> | <li>[Analysis of 3D models](/Notebooks/A5-Modeling - analysis of 3D models.ipynb)</li> |

