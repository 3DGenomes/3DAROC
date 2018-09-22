# 3DAROC

<p>
<img align="right" src=/Documents/Logo/Foto-DNA_MMarti_0.jpg?raw=True>

- [Course description](#course-description)
- [Instructors](#instructors)
- [Target Audience](#target-audience)
  - [Course Pre-requisites](#course-pre-requisites)
    - [TADbit API](#tadbit-api)
    - [TADbit tools](#tadbit-tools)
    - [Virtual research environment](#virtual-research-environment)
- [Course Timetable](#course-timetable)
- [Course material](#course-material)
- [Feedback](#feedback)
- [Thanks](#thanks)

## Course description

3C-based methods, such as Hi-C, produce a huge amount of raw data as pairs of DNA reads that are spatially close in the cell nucleus. Overall, these interaction matrices have been used to study how the genome folds within the nucleus, that is one of the most fascinating problems in modern biology. The rigorous analysis of the paired-reads using computational tools has been essential to fully exploit the experimental technique, and to study how the genome is folded in the space. Currently, there is a huge expansion on the wealth of data on genome structure with the availability of many datasets of Hi-C experiments down to 1 kb resolution (see for example: http://hic.umassmed.edu/welcome/welcome.php ; http://promoter.bx.psu.edu/hi-c/view.php or http://www.aidenlab.org/data.html ). In this course, participants will learn to use TADbit, a software designed and developed to manage all the dimensionalities of the Hi-C data:
</p>

 - 1D - Map paired-end sequences to generate Hi-C interaction matrices
 - 2D - Normalize matrices and identify constitutive domains (compartments, TADs)
 - 3D - Generate populations of model structures which reproduce the Hi-C interaction matrices
 - 4D - Compare samples at different time points

Participants can bring specific biological questions and/or their own 3C data to analyze during the course. At the end of the course, participants will be familiar with the TADbit software, and will be able to fully analyze Hi-C data. *Note: Although the TADbit software is central in this course, alternative software will be discussed for each part of the analysis.*

## Instructors

<p>
<img align="left" src=http://gtpb.igc.gulbenkian.pt/bicourses/images/Marc_Marti-Renom.jpeg?raw=True width="90">

**Marc A. Marti-Renom** obtained a Ph.D. in Biophysics from the Universidad Autonoma de Barcelona where he worked on protein folding under the supervision of B. Oliva, F.X. Aviles and M. Karplus. After that, he went to the US for a postdoctoral training on protein structure modeling at the Sali Lab (Rockefeller University) as the recipient of the Burroughs Wellcome Fund fellowship. Later on, Marc was appointed Assistant Adjunct Professor at UCSF. Between 2006 and 2011, he headed of the Structural Genomics Group at the CIPF in Valencia (Spain). Currently, Marc is an ICREA research professor and leads the Structural Genomics Group at the National Center for Genomic Analysis - Centre for Genomic Regulation (CNAG-CRG) in Barcelona. His group is broadly interested on how RNA, proteins and genomes organize and regulate cell fate. Finally, Marc is an Associate Editor of the PLoS Computational Biology journal and has published over 90 articles in international peer-reviewed journals.

*Affiliation: Centro Nacional de Análisis Genómico (CNAG) and Center for Genomic Regulation (CRG), Barcelona, ES*
</p>

<p>
<img align="left" src=http://gtpb.igc.gulbenkian.pt/bicourses/images/Francois_Serra.jpg?raw=True width="90">

**François Serra** obtained his Degree in Biology, specialized in Physiology and Neurophysiology, his Master's Degree in Structural genomics and bioinformatics (Strasbourg I University, France) and it's PhD in Evolutionary Genomics in the Department of Bioinformatics at the CIPF (Valencia). He is now part of the Structural Genomic team of Marc Marti-Renom at CNAG and at CRG (Barcelona). His main research interests are grounded on comparative genomics and evolution with a special focus on the effect of evolution in the structural arrangement of genomes. He has taught MEPA and 3DMOG for GTPB, and also in similar courses at CIPF (Valencia, ES) and the Department of Genetics of the University of Cambridge (UK).

*Affiliation: Centro Nacional de Análisis Genómico (CNAG) and Center for Genomic Regulation (CRG), Barcelona, ES*
</p>

<p>
<img align="left" src=http://gtpb.igc.gulbenkian.pt/bicourses/images/David_Castillo.JPG?raw=True width="90">

**David Castillo**  obtained his MSc in Photonics from the Universitat Politècnica de Catalunya in Barcelona (Spain) where he worked in Super-resolution microscopy. He has a background in Physics and Engineering. He works as a technician in the Structural Genomics team of Marc A. Martí-Renom at CNAG-CRG (Barcelona), developing tools for the analysis, modelling and visualization of HiC data. He is also interested in the integration of microscopy to the modeling of genomic 3D structures.

*Affiliation: Centro Nacional de Análisis Genómico (CNAG) and Center for Genomic Regulation (CRG), Barcelona, ES*
</p>

## Target Audience

The course is designed for experimental researchers and bioinformaticians at the graduate and post-graduate levels which are interested in studying the genome spatial organization. 

It is likely that the participants to this course aim at getting involved in generating Hi-C data for  chromosome structure determination, or that they just want to be able to correctly interpret and analyse publicly available data.

### Course Pre-requisites

Recommended Linux and basic Python programming skills, graduate level in Life Sciences. All hands-on will be given at 3 levels of computational expertise (web platform, command-line tool and python scripting).

#### TADbit API

This tutorial is associated with a __specific version of TADbit__, if you wish to reproduce exactly the results in the notebooks you should use the version of TADbit tagged `3DAROC_2018`.

To install this version do:

    git clone https://github.com/3dgenomes/tadbit
    cd tadbit
    git checkout tags/3DAROC_2018
    sudo python setup.py install


#### TADbit tools

Most of the tasks of the "core pipeline" can be tunned directly from command line (without any python), using [TADbit tool](/TADbit_tools). Have a look to the commands, and the metadata of the results. 

_For now TADbit tool is not incuded in the general documetation, as it is still "under construction". Use it carefully, and don't hesitate to repport any weird behaviour you observe._


#### Virtual research environment

<p>
<img align="right" src=https://www.irbbarcelona.org/sites/default/files/news/2017/07/mug2.jpg?raw=True width="160">

With small datasets TADbit core pipeline can be runned through a new Virtual Research Environment ([VRE](https://vre.multiscalegenomics.eu/workspace/)), hosted by the [MuG project](https://www.multiscalegenomics.eu/). 

This might also be the best place to try TADkit for visualizing genomes in 3D together with interactions matrices and any other genomic track.

</p>

## Course material

|                  | Lectures (pdf)                          | Core pipeline (notebooks)               | Annex (notebooks)                 |
|-------------------|----------------|-------------------------|------------|
| Day1 | <ul><li>[Welcome](/Presentations/Day1/01_20180917_Welcome.pdf)</li><li>[Intro structure determination](/Presentations/Day1/02_20180917_introduction_to_structure_determination.pdf)</li><li>[3D Genomes overview](/Presentations/Day1/03_20180917_3D-genomes_overview.pdf)</li><li>[Intro TADbit](/Presentations/Day1/04_20180917_Intro_TADbit.pdf)</li><li>[NGS for HiC](/Presentations/Day1/05_20180917_NGS_for_HiC.pdf)</li><li>[Intro UNIX](/Presentations/Day1/06_20180917_linux.pdf)</li><li>[Intro Python](/Presentations/Day1/07_20180917_python.pdf)</ul></li> |<ul><li>[Hi-C Quality check](/Notebooks/00-Hi-C%20quality%20check.ipynb)</li><li>[Mapping](/Notebooks/01-Mapping.ipynb)</li><li>[Parsing mapped reads](/Notebooks/02-Parsing%20mapped%20reads.ipynb)</li></ul> | <ul><li>[Software installation](/Notebooks/A0-Preparing%20your%20computer%20for%20HiC%20data%20analysis.ipynb)</li><li>[Prepare reference genome](/Notebooks/A1-Preparation%20reference%20genome.ipynb)</li><li>[Download Hi-C experiment](/Notebooks/A2-Download%20published%20Hi-C%20experiments.ipynb)</li></ul> |
| Day2 | <ul><li>[Morning wrap up](/Presentations/Day2/01_20180918_Summary_of_day_1.pdf)</li><li>[Chromatin and 3Cs](/Presentations/Day2/02_20180918_Chromatin_and_3Cs.pdf)</li><li>[TADbit](/Presentations/Day2/03_20180918_TADbit.pdf)</li><li>[Applications (I): Caulobacter](/Presentations/Day2/04_20180918_Applications(II)_Caulobacter.pdf)</li></ul>| <ul><li>[Filterind reads](/Notebooks/03-Filtering%20mapped%20reads.ipynb)</li><li>[Normalization](Notebooks/04-Bin-filtering%20and%20normalization.ipynb)</li></ul> | <ul><li>[Compare/merge experiments](/Notebooks/A3-Compare%20and%20merge%20Hi-C%20experiments.ipynb)</li></ul> |
| Day3 | <ul><li>[Morning wrap up](/Presentations/Day3/01_20180919_Summary_of_day_2.pdf)</li><li>[Applications(II) TAD hormone](/Presentations/Day3/02_20180919_Applications(II)_TAD_hormone.pdf)</li><li>[Applications (III) SOX2 Dynamics](/Presentations/Day3/02_20180920_Applications(IIIa)_SOX2Dynamics.pdf)</li></ul>| <ul><li>[Compartments and TADs](/Notebooks/05-Compartments%20and%20TADs.ipynb)</li></ul> | <ul><li>[Align and compare TADs](/Notebooks/A4-Align%20and%20compare%20TADs.ipynb)</li></ul> |
| Day4 | <ul><li>[Morning wrap up](/Presentations/Day4/01_20180920_Summary_of_day_3.pdf)</li><li>[Applications(IV): Super-resolution Imaging and modeling](/Presentations/Day4/03_20180920_Applications(IIIb)_IMGR.pdf)</li></ul>| <ul><li>[Parameter optimization](/Notebooks/06a-Modeling%20-%20parameter%20optimization.ipynb)</li><li>[Model optimization](/Notebooks/06b-Modeling%20-%20model%20optimization.ipynb)</li></ul> | <ul><li>[Analysis of 3D models](/Notebooks/A5-Modeling%20-%20analysis%20of%203D%20models.ipynb)</li></ul> |
| Day5 | <ul><li>[Morning wrap up](/Presentations/Day5/01_20180921_Summary_of_day_4.pdf)</li><li>[Multiscale Genomics](/Presentations/Day5/02_20180921_MuG.pdf)</li><li>[Nucleosome dynamics](/Presentations/Day5/NucDyn_3DAROC18.pdf)</li><li>[MC-DNA and Chromatin Dynamics](/Presentations/Day5/3DAROC_mcdna_chromdyn_juergenwalther_21_09_18.pdf)</li></ul> |  |

## Course Timetable

**(provisional)**

|  **Day #1**  |  **Monday, Sep 17th** |
|----|----|
|  09:30 - 10:00 	|  Welcome and introductions  |
|  10:00 - 11:00 	|  Overview on structure determination  |
|  11:00 - 11:30 	|  Coffee Break  |
|  11:30 - 12:30 	|  3D modeling of genomes and genomic domains  |
|  *12:30 - 14:00*		|  *Lunch Break*  |
|  14:00 - 15:00 	|  Introduction to Linux and Python: the Jupyter notebook  |
|  15:00 - 16:00 	|  Next Generation Sequencing (NGS) and data handling  |
|  *16:00 - 16:30* 	|  *Tea Break*  |
|  16:30 - 18:00 	|  From raw data to Hi-C contact matrices  |
|  **Day #2**  |  **Tuesday,  Sep 18th* |
|  09:30 - 10:00		|  Morning wrap-up: what have we done so far?  |
|  10:00 - 11:00		|  Chromatin structure and Hi-C data  |
|  11:00 - 11:30		|  Coffee Break  |
|  11:30 - 12:30		|  Integrative modeling applied to chromatin  |
|  *12:30 - 14:00*		|  *Lunch Break*  |
|  14:00 - 16:00		|  Biological applications (I)  |
|  16:00 - 16:30		|  *Tea Break*  |
|  *16:30 - 18:00*		|  Hi-C contact matrices: filtering and normalization  |
|  **Day #3**  |  **Wednesday, Sep 19th**  |
|  09:30 - 10:00		|  Morning wrap-up: what have we done so far?  |
|  10:00 - 11:00		|  Biological applications (II)  |
|  11:00 - 11:30		|  Coffee Break  |
|  11:30 - 12:30		|  Compartment detection and analysis  |
|  *12:30 - 14:00*		|  *Lunch Break*  |
|  14:00 - 16:00		|  Topologically Associated Domains detection and analysis  |
|  *16:00 - 16:30*		|  *Tea Break*  |
|  16:30 - 18:00		|  Comparison between experiments  |
|  **Day #4**  |  **Thursday, Sep 20th**	 |
|  09:30 - 10:00		|  Morning wrap-up: what have we done so far?  |
|  10:00 - 11:00		|  Biological applications (III)  |
|  11:00 - 11:30		|  Coffee Break  |
|  11:30 - 12:30		|  3D Modeling of real Hi-C data with TADbit (I)  |
|  *12:30 - 14:00*		|  *Lunch Break*  |
|  14:00 - 16:00		|  3D Modeling of real Hi-C data with TADbit (II)  |
|  *16:00 - 16:30*		|  *Tea Break*  |
|  16:30 - 18:00		|  Final wrap-up session  |
|  **Day #5**  |  **Friday, Sep 21st**  |
|  09:30 - 10:00		|  Morning wrap-up: what have we done so far?  |
|  10:00 - 11:00		|  Multiscale Genomics: From genomes to structures  |
|  11:00 - 11:30		|  Coffee Break  |
|  11:30 - 12:30		|  Nucleosome positioning and Nucleosome Dynamics  |
|  *12:30 - 14:00*		|  *Lunch Break*  |
|  14:00 - 16:00		|  Coarse-Grained DNA  |
|  *16:00 - 16:30* 	|  *Tea Break*  |
|  16:30 - 18:00  |  Chromatin Dynamics  |


## Feedback

|                  |  Feedback (0: not clear; 5: very clear) | |
|-------------------|------|---|
| Day1 | <dd>- UNIX/Python</dd><dd>- FASTQ/Hi-C quality before mapping </dd><dd>- Iterative vs Fragment-based mapping </dd><dd>- Stats for quality measure of Hi-C experiment </dd><dd>- Applied filters in reads </dd><dd>- Reading TADbit Hi-C map </dd> | <dd> 4.3 </dd><dd> 3.8 </dd><dd> 4.4 </dd><dd> 3.3 </dd><dd> 3.1 </dd><dd> 3.6 </dd> |
| Day2 | <dd>- What 3C-based modelling methods told us about genome</dd><dd>- 3 levels of organization (A/B, TADs, loops)</dd><dd>- Modelling 3D genomes</dd><dd>- Limits of 3D modelling</dd><dd>- TADbit filtering/normalization</dd>| <dd> 4.5 </dd><dd> 4.7 </dd><dd> 3.2 </dd><dd> 2.9 </dd><dd> 4.0 </dd>|
| Day3 | <dd>- Using TADbit tools: 3.4</dd><dd>- A/B bompartment calling: 3.3</dd><dd>- TAD calling & comparison: 3.3 </dd>| <dd>3.4</dd><dd>3.3</dd><dd>3.3 </dd> |
| Day4 | <dd>- Modeling genomes </dd>- Analyzing the 3D genomes <dd>- Reading the output of the model analysis</dd> | <dd>  2.7 </dd><dd> 2.6 </dd> <dd> 3.1 </dd> |
| Day5 |  | |

## Thanks!

<img align="right" src=3DAROC_Group.JPG?>

