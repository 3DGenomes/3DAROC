# TADbit Tools

TADbit provides a list of command-line tools that (would) allow to handle all the processing and analysis of NGS data from HiC experiments.

These command lines above would correspond to all the analysis detailed in the notebooks:

    ### yeast replica 1
    # map first end of the read to yeast reference genome (fragment based mapping). Estimated time: 7.5 min
    tadbit map -w yeast_rep1 --fastq FASTQs/yeast_rep1_1.fastq.dsrc --read 1 --index genome/R64-1-1/GEM/R64-1-1.gem --renz DpnII -C 8
    # map other end of the read to yeast reference genome (fragment based mapping). Estimated time: 7.5 min
    tadbit map -w yeast_rep1 --fastq FASTQs/yeast_rep1_yeast_2.fastq.dsrc --read 2 --index genome/R64-1-1/GEM/R64-1-1.gem --renz DpnII -C 8
    # parse mapped reads data into a new BED-like file. Estimated time: 18 min
    tadbit parse -w yeast_rep1 --genome genome/R64-1-1/R64-1-1.fa --compress_input
    # Computes the intersection of the mapping of the two ends, and filter reads
    tadbit filter -w yeast_rep1 --apply 1 2 3 4 6 7 9 10. Estimated time: 15 min
    # normalize Hi-C data. Estimated time: 1 min
    tadbit normalize -w yeast_rep1 -r 20000 --min_count 10
    
    ### yeast replica 2
    # map first end of the read to yeast reference genome (fragment based mapping). Estimated time: 7.5 min
    tadbit map -w yeast_rep2 --fastq FASTQs/yeast_rep2_1.fastq.dsrc --read 1 --index genome/R64-1-1/GEM/R64-1-1.gem --renz DpnII -C 8
    # map other end of the read to yeast reference genome (fragment based mapping). Estimated time: 7.5 min
    tadbit map -w yeast_rep2 --fastq FASTQs/yeast_rep2_2.fastq.dsrc --read 2 --index genome/R64-1-1/GEM/R64-1-1.gem --renz DpnII -C 8
    # parse mapped reads data into a new BED-like file. Estimated time: 18 min
    tadbit parse -w yeast_rep2 --genome genome/R64-1-1/R64-1-1.fa --compress_input
    # Computes the intersection of the mapping of the two ends, and filter reads
    tadbit filter -w yeast_rep2 --apply 1 2 3 4 6 7 9 10. Estimated time: 15 min
    # normalize Hi-C data. Estimated time: 1 min
    tadbit normalize -w yeast_rep2 -r 20000 --min_count 10
    
    #### merge replicas. Estimated time: 3 min
    tadbit merge -w yeast -w1 yeast_rep1 -w2 yeast_rep2 -r 20000 --norm
    # normalize Hi-C data at diferent resolutions. Estimated time: 1 min
    tadbit normalize -w yeast -r 40000 --min_count 10
    tadbit normalize -w yeast -r 20000 --min_count 10
    # search for TAD and compartments. Estimated time: 20 sec
    tadbit segment yeast -r 20000 -C 8 -j 3
    # bin Hi-C.. Estimated time: 20 sec
    tadbit bin -w yeast --norm norm --plot -r 20000 -c chrIV
    tadbit bin -w yeast --norm raw norm --plot -r 20000
    
    # Chromosomes I, II and III
    # modelling: parameter optimization. Estimated time: 6 min
    tadbit model -w yeast --optimize --beg 0 --end 1360022 --reso 20000 --maxdist 400:600:100 --upfreq=-0.2:0.2:0.1 --lowfreq=-0.4:-0.2:0.1 --nmodels 20 --nkeep 20 -j 6 --cpu 8
    # modelling: model generation. Estimated time: 2 min
    tadbit model -w yeast --model --project 3DAROC --species 'Saccharomyces cerevisiae' --assembly 'R64-1-1' --beg 0 --end 1360022 --reso 20000 --nmodels 200 --nkeep 200 -j 6 --cpu 8
    # modelling: model analysis.  Estimated time: 2 min
    tadbit model --analyze -w yeast --fig_format png -j 8

## Resulting database

Uploaded here are the folders containing the trace.db files that you can use to browse the metadata of the pipeline processed. These can be accessed with the tadbit describe tool, for example:

    $ tadbit describe yeast
    ,-------.
    | PATHs |
    ,----.-------.--------------------------------------------------------------------------------.-------------.
    | Id | JOBid |                                                                           Path |        Type |
    |----|-------|--------------------------------------------------------------------------------|-------------|
    |  1 |     1 |                                   00_merge/decay_corr_dat_20000_640dbd53bb.txt |        CORR |
    |  2 |     1 |                                   00_merge/decay_corr_dat_20000_640dbd53bb.png |      FIGURE |
    |  3 |     1 |                                   00_merge/eigen_corr_dat_20000_640dbd53bb.txt |        CORR |
    |  4 |     1 |                                   00_merge/eigen_corr_dat_20000_640dbd53bb.png |      FIGURE |
    |  5 |     1 |                              /scratch/workspace/3DAROC/TADbit_tools/yeast |     WORKDIR |
    |  6 |     1 |                                                             ../yeast_rep1 |    WORKDIR1 |
    |  7 |     1 |                                                             ../yeast_rep2 |    WORKDIR2 |
    |  8 |     1 |               ../yeast_rep1/03_filtered_reads/intersection_d83eeace6e.bam | EXT_HIC_BAM |
    |  9 |     1 |               ../yeast_rep2/03_filtered_reads/intersection_d83eeace6e.bam | EXT_HIC_BAM |
    | 10 |     1 |                                  03_filtered_reads/intersection_640dbd53bb.bam |     HIC_BAM |
    | 11 |     1 |              ../yeast_rep1/04_normalization/biases_20kb_82d3e9cd6d.pickle |      BIASES |
    | 12 |     1 |              ../yeast_rep2/04_normalization/biases_20kb_82d3e9cd6d.pickle |      BIASES |
    | 13 |     1 |      03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_random breaks.tsv |      FILTER |
    | 14 |     1 |        03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_self-circle.tsv |      FILTER |
    | 15 |     1 | 03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_too close from RES.tsv |      FILTER |
    | 16 |     1 |   03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_over-represented.tsv |      FILTER |
    | 17 |     1 |       03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_dangling-end.tsv |      FILTER |
    | 18 |     1 |          03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_too large.tsv |      FILTER |
    | 19 |     1 | 03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_extra dangling-end.tsv |      FILTER |
    | 20 |     1 |              03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_error.tsv |      FILTER |
    | 21 |     1 |          03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_too short.tsv |      FILTER |
    | 22 |     1 |         03_filtered_reads/all_r1-r2_intersection_640dbd53bb.tsv_duplicated.tsv |      FILTER |
    | 23 |     2 |                                 04_normalization/biases_40kb_5fca20987a.pickle |      BIASES |
    | 24 |     2 |                             04_normalization/filtered_bins_40kb_5fca20987a.png |      FIGURE |
    | 25 |     2 |       04_normalization/interactions_vs_genomic-coords.png_40000_5fca20987a.png |      FIGURE |
    | 26 |     3 |                                 04_normalization/biases_20kb_82d3e9cd6d.pickle |      BIASES |
    | 27 |     3 |                             04_normalization/filtered_bins_20kb_82d3e9cd6d.png |      FIGURE |
    | 28 |     3 |       04_normalization/interactions_vs_genomic-coords.png_20000_82d3e9cd6d.png |      FIGURE |
    | 29 |     4 |                          06_segmentation/compartments_20kb/chrV_32c5d19e91.tsv | COMPARTMENT |
    | 30 |     4 |                 06_segmentation/compartments_20kb/chrV_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 31 |     4 |                      06_segmentation/compartments_20kb/chrV_EV1_32c5d19e91.png |      FIGURE |
    | 32 |     4 |                                  06_segmentation/tads_20kb/chrV_32c5d19e91.tsv |         TAD |
    | 33 |     4 |                         06_segmentation/compartments_20kb/chrII_32c5d19e91.tsv | COMPARTMENT |
    | 34 |     4 |                06_segmentation/compartments_20kb/chrII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 35 |     4 |                     06_segmentation/compartments_20kb/chrII_EV1_32c5d19e91.png |      FIGURE |
    | 36 |     4 |                                 06_segmentation/tads_20kb/chrII_32c5d19e91.tsv |         TAD |
    | 37 |     4 |                         06_segmentation/compartments_20kb/chrVI_32c5d19e91.tsv | COMPARTMENT |
    | 38 |     4 |                06_segmentation/compartments_20kb/chrVI_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 39 |     4 |                     06_segmentation/compartments_20kb/chrVI_EV1_32c5d19e91.png |      FIGURE |
    | 40 |     4 |                                 06_segmentation/tads_20kb/chrVI_32c5d19e91.tsv |         TAD |
    | 41 |     4 |                        06_segmentation/compartments_20kb/chrXIV_32c5d19e91.tsv | COMPARTMENT |
    | 42 |     4 |               06_segmentation/compartments_20kb/chrXIV_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 43 |     4 |                    06_segmentation/compartments_20kb/chrXIV_EV1_32c5d19e91.png |      FIGURE |
    | 44 |     4 |                                06_segmentation/tads_20kb/chrXIV_32c5d19e91.tsv |         TAD |
    | 45 |     4 |                        06_segmentation/compartments_20kb/chrXVI_32c5d19e91.tsv | COMPARTMENT |
    | 46 |     4 |               06_segmentation/compartments_20kb/chrXVI_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 47 |     4 |                    06_segmentation/compartments_20kb/chrXVI_EV1_32c5d19e91.png |      FIGURE |
    | 48 |     4 |                                06_segmentation/tads_20kb/chrXVI_32c5d19e91.tsv |         TAD |
    | 49 |     4 |                         06_segmentation/compartments_20kb/chrXI_32c5d19e91.tsv | COMPARTMENT |
    | 50 |     4 |                06_segmentation/compartments_20kb/chrXI_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 51 |     4 |                     06_segmentation/compartments_20kb/chrXI_EV1_32c5d19e91.png |      FIGURE |
    | 52 |     4 |                                 06_segmentation/tads_20kb/chrXI_32c5d19e91.tsv |         TAD |
    | 53 |     4 |                        06_segmentation/compartments_20kb/chrVII_32c5d19e91.tsv | COMPARTMENT |
    | 54 |     4 |               06_segmentation/compartments_20kb/chrVII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 55 |     4 |                    06_segmentation/compartments_20kb/chrVII_EV1_32c5d19e91.png |      FIGURE |
    | 56 |     4 |                                06_segmentation/tads_20kb/chrVII_32c5d19e91.tsv |         TAD |
    | 57 |     4 |                         06_segmentation/compartments_20kb/chrXV_32c5d19e91.tsv | COMPARTMENT |
    | 58 |     4 |                06_segmentation/compartments_20kb/chrXV_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 59 |     4 |                     06_segmentation/compartments_20kb/chrXV_EV1_32c5d19e91.png |      FIGURE |
    | 60 |     4 |                                 06_segmentation/tads_20kb/chrXV_32c5d19e91.tsv |         TAD |
    | 61 |     4 |                         06_segmentation/compartments_20kb/chrIX_32c5d19e91.tsv | COMPARTMENT |
    | 62 |     4 |                06_segmentation/compartments_20kb/chrIX_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 63 |     4 |                     06_segmentation/compartments_20kb/chrIX_EV1_32c5d19e91.png |      FIGURE |
    | 64 |     4 |                                 06_segmentation/tads_20kb/chrIX_32c5d19e91.tsv |         TAD |
    | 65 |     4 |                          06_segmentation/compartments_20kb/chrM_32c5d19e91.tsv | COMPARTMENT |
    | 66 |     4 |                 06_segmentation/compartments_20kb/chrM_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 67 |     4 |                      06_segmentation/compartments_20kb/chrM_EV1_32c5d19e91.png |      FIGURE |
    | 68 |     4 |                        06_segmentation/compartments_20kb/chrXII_32c5d19e91.tsv | COMPARTMENT |
    | 69 |     4 |               06_segmentation/compartments_20kb/chrXII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 70 |     4 |                    06_segmentation/compartments_20kb/chrXII_EV1_32c5d19e91.png |      FIGURE |
    | 71 |     4 |                                06_segmentation/tads_20kb/chrXII_32c5d19e91.tsv |         TAD |
    | 72 |     4 |                       06_segmentation/compartments_20kb/chrXIII_32c5d19e91.tsv | COMPARTMENT |
    | 73 |     4 |              06_segmentation/compartments_20kb/chrXIII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 74 |     4 |                   06_segmentation/compartments_20kb/chrXIII_EV1_32c5d19e91.png |      FIGURE |
    | 75 |     4 |                               06_segmentation/tads_20kb/chrXIII_32c5d19e91.tsv |         TAD |
    | 76 |     4 |                        06_segmentation/compartments_20kb/chrIII_32c5d19e91.tsv | COMPARTMENT |
    | 77 |     4 |               06_segmentation/compartments_20kb/chrIII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 78 |     4 |                    06_segmentation/compartments_20kb/chrIII_EV1_32c5d19e91.png |      FIGURE |
    | 79 |     4 |                                06_segmentation/tads_20kb/chrIII_32c5d19e91.tsv |         TAD |
    | 80 |     4 |                          06_segmentation/compartments_20kb/chrX_32c5d19e91.tsv | COMPARTMENT |
    | 81 |     4 |                 06_segmentation/compartments_20kb/chrX_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 82 |     4 |                      06_segmentation/compartments_20kb/chrX_EV1_32c5d19e91.png |      FIGURE |
    | 83 |     4 |                                  06_segmentation/tads_20kb/chrX_32c5d19e91.tsv |         TAD |
    | 84 |     4 |                         06_segmentation/compartments_20kb/chrIV_32c5d19e91.tsv | COMPARTMENT |
    | 85 |     4 |                06_segmentation/compartments_20kb/chrIV_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 86 |     4 |                     06_segmentation/compartments_20kb/chrIV_EV1_32c5d19e91.png |      FIGURE |
    | 87 |     4 |                                 06_segmentation/tads_20kb/chrIV_32c5d19e91.tsv |         TAD |
    | 88 |     4 |                          06_segmentation/compartments_20kb/chrI_32c5d19e91.tsv | COMPARTMENT |
    | 89 |     4 |                 06_segmentation/compartments_20kb/chrI_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 90 |     4 |                      06_segmentation/compartments_20kb/chrI_EV1_32c5d19e91.png |      FIGURE |
    | 91 |     4 |                                  06_segmentation/tads_20kb/chrI_32c5d19e91.tsv |         TAD |
    | 92 |     4 |                       06_segmentation/compartments_20kb/chrVIII_32c5d19e91.tsv | COMPARTMENT |
    | 93 |     4 |              06_segmentation/compartments_20kb/chrVIII_EigVect1_32c5d19e91.tsv | COMPARTMENT |
    | 94 |     4 |                   06_segmentation/compartments_20kb/chrVIII_EV1_32c5d19e91.png |      FIGURE |
    | 95 |     4 |                               06_segmentation/tads_20kb/chrVIII_32c5d19e91.tsv |         TAD |
    | 96 |     5 |                                   05_sub-matrices/raw_full_20kb_46447f6d2e.abc |  RAW_MATRIX |
    | 97 |     5 |                                   05_sub-matrices/nrm_full_20kb_46447f6d2e.abc |  NRM_MATRIX |
    | 98 |     5 |                                   05_sub-matrices/raw_full_20kb_46447f6d2e.png |  RAW_FIGURE |
    | 99 |     5 |                                  05_sub-matrices/norm_full_20kb_46447f6d2e.png |  NRM_FIGURE |
    '----^-------^--------------------------------------------------------------------------------^-------------'
    ,------.
    | JOBs |
    ,----.---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------.---------------------.---------------------.-----------.----------------.
    | Id |                                                                                                                                                                                                                                                                Parameters |         Launch_time |         Finish_time |      Type | Parameters_md5 |
    |----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|---------------------|-----------|----------------|
    |  1 | force:0 cpus:24 reso:20000 samtools:samtools skip_merge:0 tmpdb1:/tmp/trace1_SKUaTggtOL tmpdb2:/tmp/trace2_HrZlhXFJTP norm:1 tmpdb:/tmp/trace_hFjRqotIoY save:genome filter:[1, 2, 3, 4, 6, 7, 9, 10] workdir1:yeast_rep1 workdir2:yeast_rep2 skip_comparison:0 | 02/09/2018 13:29:45 | 02/09/2018 13:31:40 |     Merge |     640dbd53bb |
    |  2 |                                                                                          force:0 only_valid:0 cpus:24 reso:40000 filter_only:0 fast_filter:0 factor:1 max_njobs:100 perc_zeros:95 min_count:10.0 normalization:Vanilla filter:879 seed:1 normalize_only:0 | 02/09/2018 13:33:38 | 02/09/2018 13:33:50 | Normalize |     5fca20987a |
    |  3 |                                                                                          force:0 only_valid:0 cpus:24 reso:20000 filter_only:0 fast_filter:0 factor:1 max_njobs:100 perc_zeros:95 min_count:10.0 normalization:Vanilla filter:879 seed:1 normalize_only:0 | 02/09/2018 13:33:54 | 02/09/2018 13:34:08 | Normalize |     82d3e9cd6d |
    |  4 |                                                                                                    force:0 verbose:0 nosql:0 cpus:8 reso:20000 only_compartments:0 savecorr:0 format:png all_bins:0 n_evs:3 only_tads:0 filter:[1, 2, 3, 4, 6, 7, 9, 10] fix_corr_scale:0 | 02/09/2018 13:34:11 | 02/09/2018 13:34:43 |   Segment |     32c5d19e91 |
    |  5 |                                       row_names:0 interactive:0 force:0 only_valid:0 cpus:24 reso:20000 plot:1 matrix:0 only_plot:0 force_plot:0 bad_color:white xtick_rotation:-25 normalizations:[raw, norm] format:png triangular:0 only_txt:0 filter:879 cmap:viridis | 02/09/2018 13:34:59 | 02/09/2018 13:35:47 |       Bin |     46447f6d2e |
    '----^---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------^---------------------^---------------------^-----------^----------------'
    ,----------------.
    | FILTER_OUTPUTs |
    ,----.--------.--------------------.------------.-------.
    | Id | PATHid |               Name |      Count | JOBid |
    |----|--------|--------------------|------------|-------|
    |  1 |     10 |        valid-pairs |  7,863,688 |     1 |
    |  2 |     13 |      random breaks | 21,240,182 |     1 |
    |  3 |     14 |        self-circle |     21,439 |     1 |
    |  4 |     15 | too close from RES | 16,095,726 |     1 |
    |  5 |     16 |   over-represented |    545,763 |     1 |
    |  6 |     17 |       dangling-end |  4,054,353 |     1 |
    |  7 |     18 |          too large |          0 |     1 |
    |  8 |     19 | extra dangling-end |  5,268,348 |     1 |
    |  9 |     20 |              error | 29,540,980 |     1 |
    | 10 |     21 |          too short |  2,562,426 |     1 |
    | 11 |     22 |         duplicated | 19,162,672 |     1 |
    '----^--------^--------------------^------------^-------'
    ,---------------.
    | MERGE_OUTPUTs |
    ,----.-------.-----------.-----------.----------.----------.-----------.
    | Id | JOBid | Wrkd1Path | Wrkd2Path | Bed1Path | Bed2Path | MergePath |
    |----|-------|-----------|-----------|----------|----------|-----------|
    |  1 |     1 |         6 |         7 |        8 |        9 |        10 |
    '----^-------^-----------^-----------^----------^----------^-----------'
    ,-------------.
    | MERGE_STATs |
    ,----.-------.--------.----------------.-----------------.-----------.------------.------------.-----------.-----------.
    | Id | JOBid | Inputs |     decay_corr |      eigen_corr | N_columns | N_filtered | Resolution | bias1Path | bias2Path |
    |----|-------|--------|----------------|-----------------|-----------|------------|------------|-----------|-----------|
    |  1 |     1 |   None | .8-.6-.6-.6-.6 | .99-.87-.44-.55 |       616 |          4 |     20,000 |        11 |        12 |
    '----^-------^--------^----------------^-----------------^-----------^------------^------------^-----------^-----------'
    ,-------------------.
    | NORMALIZE_OUTPUTs |
    ,----.-------.-------.-----------.------------.------------.--------------------.---------------------.------------------.------------.---------------.--------.
    | Id | JOBid | Input | N_columns | N_filtered | BAM_filter | Cis_percentage_Raw | Cis_percentage_Norm | Slope_700kb_10Mb | Resolution | Normalization | Factor |
    |----|-------|-------|-----------|------------|------------|--------------------|---------------------|------------------|------------|---------------|--------|
    |  1 |     2 |    10 |       312 |          0 |        879 |          43.601678 |           30.652997 |        -0.107225 |     40,000 |       Vanilla |      1 |
    |  2 |     3 |    10 |       616 |          0 |        879 |          43.601602 |           35.054666 |        -0.068843 |     20,000 |       Vanilla |      1 |
    '----^-------^-------^-----------^------------^------------^--------------------^---------------------^------------------^------------^---------------^--------'
    ,-----------------.
    | SEGMENT_OUTPUTs |
    ,----.-------.--------.------.--------------.------------.----------.---------------.------------.------------.
    | Id | JOBid | Inputs | TADs | Compartments | richA_corr | EV_index |        EValue | Chromosome | Resolution |
    |----|-------|--------|------|--------------|------------|----------|---------------|------------|------------|
    |  1 |     4 |  26,10 |    5 |            3 |       None |        1 | 12.3102377117 |       chrV |     20,000 |
    |  2 |     4 |  26,10 |    6 |            3 |       None |        1 | 18.7719417651 |      chrII |     20,000 |
    |  3 |     4 |  26,10 |    2 |            4 |       None |        1 | 5.44670235757 |      chrVI |     20,000 |
    |  4 |     4 |  26,10 |    7 |            3 |       None |        1 | 15.8518813355 |     chrXIV |     20,000 |
    |  5 |     4 |  26,10 |    7 |            3 |       None |        1 | 21.9055182663 |     chrXVI |     20,000 |
    |  6 |     4 |  26,10 |    5 |            3 |       None |        1 | 13.6548500062 |      chrXI |     20,000 |
    |  7 |     4 |  26,10 |    9 |            3 |       None |        1 | 22.9077334238 |     chrVII |     20,000 |
    |  8 |     4 |  26,10 |   10 |           18 |       None |        1 | 20.0942652852 |      chrXV |     20,000 |
    |  9 |     4 |  26,10 |    4 |           10 |       None |        1 | 12.6245372684 |      chrIX |     20,000 |
    | 10 |     4 |  26,10 | None |            3 |       None |        1 |  2.5360022218 |       chrM |     20,000 |
    | 11 |     4 |  26,10 |    8 |            2 |       None |        1 | 21.7181473623 |     chrXII |     20,000 |
    | 12 |     4 |  26,10 |    8 |            3 |       None |        1 | 19.2593472413 |    chrXIII |     20,000 |
    | 13 |     4 |  26,10 |    3 |            3 |       None |        1 | 7.02349204184 |     chrIII |     20,000 |
    | 14 |     4 |  26,10 |    4 |           16 |       None |        1 | 10.3721900897 |       chrX |     20,000 |
    | 15 |     4 |  26,10 |   12 |            3 |       None |        1 | 37.0744366388 |      chrIV |     20,000 |
    | 16 |     4 |  26,10 |    2 |            3 |       None |        1 | 3.93673211198 |       chrI |     20,000 |
    | 17 |     4 |  26,10 |    5 |            3 |       None |        1 | 14.8085778982 |    chrVIII |     20,000 |
    '----^-------^--------^------^--------------^------------^----------^---------------^------------^------------'
