# TADbit Tools

TADbit provides a list of command-line tools that (would) allow to handle all the processing and analysis of NGS data from HiC experiments.

These command lines above would correspond to all the analysis detailed in the notebooks:

    tadbit map -w HindIII_T0 --fastq FASTQs/Hi-C_HindIII_T0_1.fastq.dsrc --read 1 --index genome/Homo_sapiens_contigs.gem --renz HindIII -C 8
    tadbit map -w HindIII_T0 --fastq FASTQs/Hi-C_HindIII_T0_2.fastq.dsrc --read 2 --index genome/Homo_sapiens_contigs.gem --renz HindIII -C 8
    tadbit map -w NcoI_T0 --fastq FASTQs/Hi-C_NcoI_T0_1.fastq.dsrc --read 1 --index genome/Homo_sapiens_contigs.gem --renz NcoI -C 8
    tadbit map -w NcoI_T0 --fastq FASTQs/Hi-C_NcoI_T0_2.fastq.dsrc --read 2 --index genome/Homo_sapiens_contigs.gem --renz NcoI -C 8
    tadbit parse -w HindIII_T0 --genome genome/Homo_sapiens_contigs.fa --compress_input
    tadbit parse -w NcoI_T0 --genome genome/Homo_sapiens_contigs.fa --compress_input
    tadbit filter -w HindIII_T0
    tadbit filter -w NcoI_T0
    tadbit normalize -w HindIII_T0 -r 300000 --min_count 10
    tadbit normalize -w NcoI_T0 -r 300000 --min_count 10
    tadbit merge -w both_T0 -w1 HindIII_T0 -w2 NcoI_T0 -r 300000 --perc_zeros 100 --norm --tmpdb /tmp
    tadbit normalize -w both_T0 -r 300000 --min_count 10
    tadbit normalize -w both_T0 -r 100000 --min_count 10
    tadbit segment both_T0 -r 100000 -C 8 -c 18 19 20 -j 3
    tadbit model both_T0 --optimize --maxdist 1000:2000:500 --upfreq 0:0.6:0.3 --lowfreq=-0.9:0:0.3 --dcutoff 1.5 2 -r 100000 --crm 18 --beg 68500000 --end 75000000 --input_matrix both_T0/04_normalization/intra_chromosome_nrm_matrices_100000_d31222bc2d/18.mat
