# TADbit Tools

TADbit provides a list of command-line tools that (would) allow to handle all the processing and analysis of NGS data from HiC experiments.

These command lines above would correspond to all the analysis detailed in the notebooks:

    ### HindIII
    # map first end of the read to human reference genome (fragment based mapping)
    tadbit map -w HindIII_T0 --fastq FASTQs/Hi-C_HindIII_T0_1.fastq.dsrc --read 1 --index genome/Homo_sapiens_contigs.gem --renz HindIII -C 8
    # map other end of the read to human reference genome (fragment based mapping)
    tadbit map -w HindIII_T0 --fastq FASTQs/Hi-C_HindIII_T0_2.fastq.dsrc --read 2 --index genome/Homo_sapiens_contigs.gem --renz HindIII -C 8
    # parse mapped reads data into a new BED-like file
    tadbit parse -w HindIII_T0 --genome genome/Homo_sapiens_contigs.fa --compress_input
    # Computes the intersection of the mapping of the two ends, and filter reads
    tadbit filter -w HindIII_T0 --apply 1 2 3 4 5 6 7 8 9 10
    # normalize Hi-C data
    tadbit normalize -w HindIII_T0 -r 300000 --min_count 10
    ### NcoI
    # map first end of the read to human reference genome (fragment based mapping)
    tadbit map -w NcoI_T0 --fastq FASTQs/Hi-C_NcoI_T0_1.fastq.dsrc --read 1 --index genome/Homo_sapiens_contigs.gem --renz NcoI -C 8
    # map other end of the read to human reference genome (fragment based mapping)
    tadbit map -w NcoI_T0 --fastq FASTQs/Hi-C_NcoI_T0_2.fastq.dsrc --read 2 --index genome/Homo_sapiens_contigs.gem --renz NcoI -C 8
    # parse mapped reads data into a new BED-like file
    tadbit parse -w NcoI_T0 --genome genome/Homo_sapiens_contigs.fa --compress_input
    # Computes the intersection of the mapping of the two ends, and filter reads
    tadbit filter -w NcoI_T0 --apply 1 2 3 4 5 6 7 8 9 10
    # normalize Hi-C data
    tadbit normalize -w NcoI_T0 -r 300000 --min_count 10

    #### merge HindIII and NcoI experiments
    tadbit merge -w both_T0 -w1 HindIII_T0 -w2 NcoI_T0 -r 300000 --perc_zeros 100 --norm --tmpdb /tmp
    # normalize Hi-C data at diferent resolutions
    tadbit normalize -w both_T0 -r 300000 --min_count 10
    tadbit normalize -w both_T0 -r 100000 --min_count 10
    # search for TAD and compartments
    tadbit segment both_T0 -r 100000 -C 8 -c 18 19 20 -j 3
    # modelling: parameter optimization
    tadbit model both_T0 --optimize --maxdist 1000:2000:500 --upfreq 0:0.6:0.3 --lowfreq=-0.9:0:0.3 --dcutoff 1.5 2 -r 100000 --crm 18 --beg 68500000 --end 75000000 --input_matrix both_T0/04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d/18.mat  -C 8 --nmodels 40 --nkeep 20
    # modelling: model generation
    tadbit model both_T0 --maxdist 1000:2000:500 --upfreq 0:0.6:0.3 --lowfreq=-0.9:0:0.3 --dcutoff 1.5 2 -r 100000 --crm 18 --beg 68500000 --end 75000000 --input_matrix both_T0/04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d/18.mat -C 8 --nmodels 500 --nkeep 100


## Resulting database

Uploaded here are the folders containing the trace.db files that you can use to browse the metadata of the pipeline processed. These can be accessed with the tadbit describe tool, for example:

    $ tadbit describe both_T0
    ,-------.
    | PATHs |
    ,----.-------.--------------------------------------------------------------------------------.--------------.
    | Id | JOBid |                                                                           Path |         Type |
    |----+-------+--------------------------------------------------------------------------------+--------------|
    |  1 |     1 |                                  00_merge/decay_corr_dat_300000_f69b503b1b.txt |         CORR |
    |  2 |     1 |                                  00_merge/decay_corr_dat_300000_f69b503b1b.png |       FIGURE |
    |  3 |     1 |                                  00_merge/eigen_corr_dat_300000_f69b503b1b.txt |         CORR |
    |  4 |     1 |                                  00_merge/eigen_corr_dat_300000_f69b503b1b.png |       FIGURE |
    |  5 |     1 |        /home/fransua/Notebooks/Tutorials/Courses/2016_3DAROC/Notebooks/both_T0 |      WORKDIR |
    |  6 |     1 |                                                                  ../HindIII_T0 |     WORKDIR1 |
    |  7 |     1 |                                                                     ../NcoI_T0 |     WORKDIR2 |
    |  8 |     1 |        ../HindIII_T0/03_filtered_reads/valid_r1-r2_intersection_b51cdf1282.tsv |       2D_BED |
    |  9 |     1 |           ../NcoI_T0/03_filtered_reads/valid_r1-r2_intersection_b51cdf1282.tsv |       2D_BED |
    | 10 |     1 |                      03_filtered_reads/valid_r1-r2_intersection_f69b503b1b.tsv |       2D_BED |
    | 11 |     1 |                      ../HindIII_T0/04_normalization/bias_300000_e3af225096.tsv |       BIASES |
    | 12 |     1 |         ../HindIII_T0/04_normalization/bad_columns_300000_95_10_e3af225096.tsv |  BAD_COLUMNS |
    | 13 |     1 |                         ../NcoI_T0/04_normalization/bias_300000_e3af225096.tsv |       BIASES |
    | 14 |     1 |            ../NcoI_T0/04_normalization/bad_columns_300000_95_10_e3af225096.tsv |  BAD_COLUMNS |
    | 15 |     1 |      03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_random breaks.tsv |       FILTER |
    | 16 |     1 |        03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_self-circle.tsv |       FILTER |
    | 17 |     1 | 03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_too close from RES.tsv |       FILTER |
    | 18 |     1 |   03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_over-represented.tsv |       FILTER |
    | 19 |     1 |       03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_dangling-end.tsv |       FILTER |
    | 20 |     1 |          03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_too large.tsv |       FILTER |
    | 21 |     1 | 03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_extra dangling-end.tsv |       FILTER |
    | 22 |     1 |              03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_error.tsv |       FILTER |
    | 23 |     1 |          03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_too short.tsv |       FILTER |
    | 24 |     1 |         03_filtered_reads/all_r1-r2_intersection_f69b503b1b.tsv_duplicated.tsv |       FILTER |
    | 25 |     2 |                              04_normalization/hic-data_300kb_e3af225096.pickle |       PICKLE |
    | 26 |     2 |                       04_normalization/bad_columns_300000_95_10_e3af225096.tsv |  BAD_COLUMNS |
    | 27 |     2 |                                    04_normalization/bias_300000_e3af225096.tsv |       BIASES |
    | 28 |     2 |      04_normalization/interactions_vs_genomic-coords.pdf_300000_e3af225096.pdf |       FIGURE |
    | 29 |     2 |                 04_normalization/intra_chromosome_nrm_images_300000_e3af225096 |      FIGURES |
    | 30 |     2 |               04_normalization/intra_chromosome_nrm_matrices_300000_e3af225096 | NRM_MATRICES |
    | 31 |     2 |                        04_normalization/genomic_maps_nrm_300000_e3af225096.pdf |       FIGURE |
    | 32 |     2 |                             04_normalization/genomic_nrm_300000_e3af225096.tsv |   NRM_MATRIX |
    | 33 |     2 |                 04_normalization/intra_chromosome_raw_images_300000_e3af225096 |      FIGURES |
    | 34 |     2 |               04_normalization/intra_chromosome_raw_matrices_300000_e3af225096 | RAW_MATRICES |
    | 35 |     2 |                        04_normalization/genomic_maps_raw_300000_e3af225096.pdf |       FIGURE |
    | 36 |     2 |                             04_normalization/genomic_raw_300000_e3af225096.tsv |   RAW_MATRIX |
    | 37 |     3 |                              04_normalization/hic-data_100kb_d31222bc2d.pickle |       PICKLE |
    | 38 |     3 |                       04_normalization/bad_columns_100000_95_10_d31222bc2d.tsv |  BAD_COLUMNS |
    | 39 |     3 |                                    04_normalization/bias_100000_d31222bc2d.tsv |       BIASES |
    | 40 |     3 |      04_normalization/interactions_vs_genomic-coords.pdf_100000_d31222bc2d.pdf |       FIGURE |
    | 41 |     3 |                 04_normalization/intra_chromosome_nrm_images_100000_d31222bc2d |      FIGURES |
    | 42 |     3 |               04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d | NRM_MATRICES |
    | 43 |     3 |                        04_normalization/genomic_maps_nrm_100000_d31222bc2d.pdf |       FIGURE |
    | 44 |     3 |                             04_normalization/genomic_nrm_100000_d31222bc2d.tsv |   NRM_MATRIX |
    | 45 |     3 |                 04_normalization/intra_chromosome_raw_images_100000_d31222bc2d |      FIGURES |
    | 46 |     3 |               04_normalization/intra_chromosome_raw_matrices_100000_d31222bc2d | RAW_MATRICES |
    | 47 |     3 |                        04_normalization/genomic_maps_raw_100000_d31222bc2d.pdf |       FIGURE |
    | 48 |     3 |                             04_normalization/genomic_raw_100000_d31222bc2d.tsv |   RAW_MATRIX |
    | 49 |     4 |                           05_segmentation/compartments_100kb/19_e13fd96b46.tsv |  COMPARTMENT |
    | 50 |     4 |                                   05_segmentation/tads_100kb/19_e13fd96b46.tsv |          TAD |
    | 51 |     4 |                           05_segmentation/compartments_100kb/18_e13fd96b46.tsv |  COMPARTMENT |
    | 52 |     4 |                                   05_segmentation/tads_100kb/18_e13fd96b46.tsv |          TAD |
    | 53 |     4 |                           05_segmentation/compartments_100kb/20_e13fd96b46.tsv |  COMPARTMENT |
    | 54 |     4 |                                   05_segmentation/tads_100kb/20_e13fd96b46.tsv |          TAD |
    | 55 |     5 |                                              06_model/8c9b82bc79_chr18_685-750 |          DIR |
    '----^-------^--------------------------------------------------------------------------------^--------------'
    ,------.
    | JOBs |
    ,----.------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------.---------------------.---------------------.-----------.----------------.
    | Id |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Parameters |         Launch_time |         Finish_time |      Type | Parameters_md5 |
    |----+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+---------------------+-----------+----------------|
    |  1 |                                                                                                                                                                                                                                                                                                                         force:0 reso:300000 skip_merge:0 tmpdb1:/tmp/trace1_aOgMRPExAV save:genome perc_zeros:100.0 tmpdb:/tmp/trace_sAmxLVYdbD norm:1 tmpdb2:/tmp/trace2_kZVysocLDx skip_comparison:0 workdir1:HindIII_T0 workdir2:NcoI_T0 resolution:ICE | 13/10/2016 09:41:42 | 13/10/2016 09:59:54 |     Merge |     f69b503b1b |
    |  2 |                                                                                                                                                                                                                                                                                                                                                                                                                    force:0 filter_only:0 fast_filter:0 reso:300000 factor:1 normalization:ICE min_count:10.0 keep:[intra, genome] perc_zeros:95 only_txt:0 | 13/10/2016 10:34:56 | 13/10/2016 11:00:48 | Normalize |     e3af225096 |
    |  3 |                                                                                                                                                                                                                                                                                                                                                                                                                    force:0 filter_only:0 fast_filter:0 reso:100000 factor:1 normalization:ICE min_count:10.0 keep:[intra, genome] perc_zeros:95 only_txt:0 | 13/10/2016 10:35:05 | 13/10/2016 12:55:06 | Normalize |     d31222bc2d |
    |  4 |                                                                                                                                                                                                                                                                                                                                                                                                                                                 crms:[18, 19, 20] nosql:0 cpus:8 only_compartments:0 force:0 jobid:3 only_tads:0 perc_zeros:95 reso:100000 | 13/10/2016 14:43:32 | 13/10/2016 14:52:15 |   Segment |     e13fd96b46 |
    |  5 |     rand:1 upfreq:(0.0, 0.29999999999999999, 0.59999999999999998) cpus:8 nkeep:20 nmodels:80 reso:100000 nmodels_run:80 scale:(0.01,) end:750 matrix:/home/fransua/Notebooks/Tutorials/Courses/2016_3DAROC/Notebooks/both_T0/04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d/18.mat lowfreq:(-0.90000000000000002, -0.60000000000000009, -0.30000000000000016, -2.2204460492503131e-16) ori_beg:68500000.0 analyze:0 maxdist:(1000, 1500, 2000) dcutoff:(1.5, 2.0) perc_zero:90.0 optimize:1 beg:685 job_list:0 ori_end:75000000.0 crm:18 | 14/10/2016 12:19:21 | 14/10/2016 13:05:12 |     OPTIM |     d24c5554a3 |
    |  6 | rand:82 upfreq:(0.0, 0.29999999999999999, 0.59999999999999998) cpus:8 nkeep:100 nmodels:420 reso:100000 nmodels_run:500 scale:(0.01,) end:750 matrix:/home/fransua/Notebooks/Tutorials/Courses/2016_3DAROC/Notebooks/both_T0/04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d/18.mat lowfreq:(-0.90000000000000002, -0.60000000000000009, -0.30000000000000016, -2.2204460492503131e-16) ori_beg:68500000.0 analyze:0 maxdist:(1000, 1500, 2000) dcutoff:(1.5, 2.0) perc_zero:90.0 optimize:0 beg:685 job_list:0 ori_end:75000000.0 crm:18 | 14/10/2016 13:24:10 | 14/10/2016 13:31:09 |     MODEL |     667e751bda |
    '----^------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------^---------------------^---------------------^-----------^----------------'
    ,----------------.
    | FILTER_OUTPUTs |
    ,----.--------.--------------------.----------.-------.
    | Id | PATHid |               Name |    Count | JOBid |
    |----+--------+--------------------+----------+-------|
    |  1 |     10 |        valid-pairs | 30615902 |     1 |
    |  2 |     15 |      random breaks |  3079332 |     1 |
    |  3 |     16 |        self-circle |   507413 |     1 |
    |  4 |     17 | too close from RES |  6904926 |     1 |
    |  5 |     18 |   over-represented |   598392 |     1 |
    |  6 |     19 |       dangling-end |  1645058 |     1 |
    |  7 |     20 |          too large |     5517 |     1 |
    |  8 |     21 | extra dangling-end |  7290143 |     1 |
    |  9 |     22 |              error |    29737 |     1 |
    | 10 |     23 |          too short |   288854 |     1 |
    | 11 |     24 |         duplicated |  2331281 |     1 |
    '----^--------^--------------------^----------^-------'
    ,-------------------.
    | NORMALIZE_OUTPUTs |
    ,----.-------.-------.-----------.------------.------------------.------------------.------------------.------------------.------------------.------------.--------.
    | Id | JOBid | Input | N_columns | N_filtered | CisTrans_nrm_all | CisTrans_nrm_out | CisTrans_raw_all | CisTrans_raw_out | Slope_700kb_10Mb | Resolution | Factor |
    |----+-------+-------+-----------+------------+------------------+------------------+------------------+------------------+------------------+------------+--------|
    |  1 |     2 |    10 |     10307 |       1013 |         0.454026 |         0.370601 |         0.425948 |         0.345169 |        -1.276506 |     300000 |      1 |
    |  2 |     3 |    10 |     30895 |       3333 |          0.45603 |         0.409415 |         0.425826 |         0.379802 |        -1.123703 |     100000 |      1 |
    '----^-------^-------^-----------^------------^------------------^------------------^------------------^------------------^------------------^------------^--------'
    ,-----------------.
    | SEGMENT_OUTPUTs |
    ,----.-------.----------.------.--------------.------------.------------.
    | Id | JOBid |   Inputs | TADs | Compartments | Chromosome | Resolution |
    |----+-------+----------+------+--------------+------------+------------|
    |  1 |     4 | 38,39,10 |   40 |           24 |         19 |     100000 |
    |  2 |     4 | 38,39,10 |   54 |           21 |         18 |     100000 |
    |  3 |     4 | 38,39,10 |   43 |           15 |         20 |     100000 |
    '----^-------^----------^------^--------------^------------^------------'
    ,-----------------.
    | MODELED_REGIONs |
    ,----.--------.------------.--------.-----.-----.
    | Id | PATHid |  PARAM_md5 |   RESO | BEG | END |
    |----+--------+------------+--------+-----+-----|
    |  1 |     55 | 8c9b82bc79 | 100000 | 685 | 750 |
    '----^--------^------------^--------^-----^-----'
    ,--------.
    | MODELs |
    ,----.----------.-------.--------------.---------.--------.---------.-------.--------.---------.------.-------------.
    | Id | REGIONid | JOBid |   OPTPAR_md5 | MaxDist | UpFreq | LowFreq | Scale | Cutoff | Nmodels | Kept | Correlation |
    |----+----------+-------+--------------+---------+--------+---------+-------+--------+---------+------+-------------|
    |  1 |        1 |     5 | e9de26ffaf06 |    1000 |    0.3 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.756294 |
    |  2 |        1 |     5 | 750db137b2d1 |    1500 |      0 |       0 |  0.01 |      2 |      80 |   20 |    0.762321 |
    |  3 |        1 |     5 | dda9d1aeb287 |    2000 |    0.6 |       0 |  0.01 |      2 |      80 |   20 |    0.760917 |
    |  4 |        1 |     5 | c07e5230032f |    2000 |      0 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.767497 |
    |  5 |        1 |     5 | 458142625b75 |    2000 |      0 |       0 |  0.01 |    1.5 |      80 |   20 |    0.777149 |
    |  6 |        1 |     5 | 7622e1b4237f |    1000 |    0.3 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.749254 |
    |  7 |        1 |     5 | d9e781cf4b0d |    2000 |    0.3 |       0 |  0.01 |    1.5 |      80 |   20 |    0.780612 |
    |  8 |        1 |     5 | e447de564717 |    2000 |    0.3 |    -0.3 |  0.01 |      2 |      80 |   20 |     0.77928 |
    |  9 |        1 |     5 | a654bb9de27b |    2000 |    0.3 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.776365 |
    | 10 |        1 |     5 | 478040030aa6 |    1000 |    0.3 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.757046 |
    | 11 |        1 |     5 | 4851b5b9466a |    1000 |    0.3 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.760546 |
    | 12 |        1 |     5 | a66765e2427b |    1000 |    0.3 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.750835 |
    | 13 |        1 |     5 | 71d7ab142a43 |    1500 |    0.6 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.740126 |
    | 14 |        1 |     5 | e6a5b65b3455 |    2000 |    0.6 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.757808 |
    | 15 |        1 |     5 | 7aac515c2565 |    1000 |    0.3 |       0 |  0.01 |    1.5 |      80 |   20 |    0.744847 |
    | 16 |        1 |     5 | 299175d71874 |    1500 |      0 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.768979 |
    | 17 |        1 |     5 | e12160273a55 |    1000 |      0 |       0 |  0.01 |      2 |      80 |   20 |    0.751748 |
    | 18 |        1 |     5 | 9194785a7d79 |    2000 |    0.6 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.764916 |
    | 19 |        1 |     5 | 3a79d25706a6 |    1500 |    0.6 |    -0.3 |  0.01 |      2 |      80 |   20 |     0.75549 |
    | 20 |        1 |     5 | edcc9e2d4f7e |    1000 |      0 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.747057 |
    | 21 |        1 |     5 | 17ef7a306618 |    1500 |      0 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.762152 |
    | 22 |        1 |     5 | 294ad7a92a15 |    1500 |      0 |       0 |  0.01 |    1.5 |      80 |   20 |    0.745106 |
    | 23 |        1 |     5 | e4d2b9667f15 |    1500 |    0.6 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.742847 |
    | 24 |        1 |     5 | e39923993794 |    1000 |      0 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.745945 |
    | 25 |        1 |     5 | 659b368e7c74 |    2000 |    0.3 |       0 |  0.01 |      2 |      80 |   20 |     0.77197 |
    | 26 |        1 |     5 | 499863ce06a9 |    1500 |    0.3 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.749441 |
    | 27 |        1 |     5 | 614a719c9ca9 |    1000 |      0 |       0 |  0.01 |    1.5 |      80 |   20 |    0.742791 |
    | 28 |        1 |     5 | 2154f4b10bc7 |    1500 |    0.3 |       0 |  0.01 |      2 |      80 |   20 |    0.771914 |
    | 29 |        1 |     5 | 05fc433ac74c |    1500 |    0.6 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.760136 |
    | 30 |        1 |     5 | 77e38c6b758e |    1500 |      0 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.739877 |
    | 31 |        1 |     5 | fa691d34b74e |    2000 |    0.3 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.768678 |
    | 32 |        1 |     5 | ef81d5407076 |    1500 |    0.3 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.740605 |
    | 33 |        1 |     5 | 62ab8cf37e29 |    1500 |    0.3 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.744827 |
    | 34 |        1 |     5 | 41f3f544aea2 |    2000 |      0 |    -0.3 |  0.01 |    1.5 |      80 |   20 |     0.76693 |
    | 35 |        1 |     5 | 8702c67a69e0 |    1500 |    0.3 |       0 |  0.01 |    1.5 |      80 |   20 |    0.747833 |
    | 36 |        1 |     5 | e1fee4941769 |    2000 |    0.6 |       0 |  0.01 |    1.5 |      80 |   20 |    0.770151 |
    | 37 |        1 |     5 | a9114df2dd74 |    1000 |    0.3 |       0 |  0.01 |      2 |      80 |   20 |    0.750416 |
    | 38 |        1 |     5 | d8681e7c4352 |    2000 |      0 |       0 |  0.01 |      2 |      80 |   20 |    0.770243 |
    | 39 |        1 |     5 | 3c7ad3619e93 |    1000 |    0.6 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.741154 |
    | 40 |        1 |     5 | 975736166336 |    1500 |      0 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.743625 |
    | 41 |        1 |     5 | 2d338ea66c6b |    1000 |      0 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.747074 |
    | 42 |        1 |     5 | e8fb62703ae1 |    1500 |    0.3 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.765901 |
    | 43 |        1 |     5 | 5271f12571ae |    1000 |    0.6 |       0 |  0.01 |      2 |      80 |   20 |    0.749339 |
    | 44 |        1 |     5 | eb3f4d69137f |    1500 |    0.3 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.770473 |
    | 45 |        1 |     5 | b2c352178958 |    1000 |    0.6 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.744126 |
    | 46 |        1 |     5 | c8cfbbbef107 |    2000 |    0.6 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.769087 |
    | 47 |        1 |     5 | 7b93e961f1ca |    1500 |    0.6 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.737931 |
    | 48 |        1 |     5 | 030e4e30a13e |    1000 |      0 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.743411 |
    | 49 |        1 |     5 | 127bd1733460 |    1000 |    0.3 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.746362 |
    | 50 |        1 |     5 | b9dab3b0c026 |    2000 |      0 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.764604 |
    | 51 |        1 |     5 | d503d231414c |    1000 |    0.6 |    -0.9 |  0.01 |    1.5 |      80 |   20 |    0.736944 |
    | 52 |        1 |     5 | a9488aefff29 |    1500 |    0.6 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.761183 |
    | 53 |        1 |     5 | a4be8b854de2 |    1000 |      0 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.743641 |
    | 54 |        1 |     5 | 9b7190093cbb |    2000 |    0.6 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.764423 |
    | 55 |        1 |     5 | b881919b7ec9 |    2000 |      0 |    -0.3 |  0.01 |      2 |      80 |   20 |     0.77263 |
    | 56 |        1 |     5 | 9561d8015892 |    1500 |      0 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.772466 |
    | 57 |        1 |     5 | b8948d8fee68 |    2000 |    0.6 |    -0.3 |  0.01 |    1.5 |      80 |   20 |     0.76964 |
    | 58 |        1 |     5 | 83fbcc753cff |    1000 |    0.6 |       0 |  0.01 |    1.5 |      80 |   20 |    0.740705 |
    | 59 |        1 |     5 | 445b6f9088d9 |    1000 |      0 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.745744 |
    | 60 |        1 |     5 | 418825bb59c4 |    2000 |    0.3 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.781529 |
    | 61 |        1 |     5 | 69262587961d |    1000 |    0.6 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.746539 |
    | 62 |        1 |     5 | b8cceb347eae |    1000 |    0.6 |    -0.3 |  0.01 |      2 |      80 |   20 |    0.746553 |
    | 63 |        1 |     5 | afa3e615fb4c |    1500 |    0.6 |       0 |  0.01 |      2 |      80 |   20 |    0.759346 |
    | 64 |        1 |     5 | 73ce881b5b98 |    2000 |    0.6 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.764907 |
    | 65 |        1 |     5 | 33047c6785af |    2000 |    0.3 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.777297 |
    | 66 |        1 |     5 | 2779d672face |    2000 |      0 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.767198 |
    | 67 |        1 |     5 | 4025290d1344 |    1000 |    0.6 |    -0.9 |  0.01 |      2 |      80 |   20 |    0.743615 |
    | 68 |        1 |     5 | 9a8c40292403 |    2000 |    0.3 |    -0.6 |  0.01 |    1.5 |      80 |   20 |    0.767246 |
    | 69 |        1 |     5 | fc29bebe50a2 |    2000 |      0 |    -0.9 |  0.01 |      2 |      80 |   20 |     0.77867 |
    | 70 |        1 |     5 | f11baca97dd0 |    1500 |      0 |    -0.3 |  0.01 |    1.5 |      80 |   20 |    0.737911 |
    | 71 |        1 |     5 | 85809b017a8d |    1500 |    0.3 |    -0.6 |  0.01 |      2 |      80 |   20 |    0.765391 |
    | 72 |        1 |     5 | b9d58f19e150 |    1500 |    0.6 |       0 |  0.01 |    1.5 |      80 |   20 |    0.749536 |
    '----^----------^-------^--------------^---------^--------^---------^-------^--------^---------^------^-------------'

