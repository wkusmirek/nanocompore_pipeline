# How to run
wget -qO- https://github.com/nextflow-io/nextflow/releases/download/v22.10.4/nextflow | bash
./nextflow run nanocompore.nf

python3 compress_fast5.py --input_path experiment20231117_no_modification/fast5_vbz --save_path experiment20231117_no_modification/fast5 --compression gzip --recursive --threads 4
python3 compress_fast5.py --input_path experiment20231120_ncm5SU_long/fast5_vbz --save_path experiment20231120_ncm5SU_long/fast5 --compression gzip --recursive --threads 4

docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/genomics_tools:1.0.1 samtools faidx unmodified_all_all_all_rna_sequences_LYS.fasta

==============================================
====== experiment20231117_no_modification ====
==============================================
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'minimap2 -x map-ont -t 4 -a unmodified_all_all_all_rna_sequences_LYS.fasta experiment20231117_no_modification/guppy/pass/*.fastq > experiment20231117_no_modification/minimap.sam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools view experiment20231117_no_modification/minimap.sam -bh -t unmodified_all_all_all_rna_sequences_LYS.fasta.fai -F 2324 | samtools sort -@ 4 -o experiment20231117_no_modification/minimap.filt.sort.bam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools index experiment20231117_no_modification/minimap.filt.sort.bam experiment20231117_no_modification/minimap.filt.sort.bam.bai'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'cat experiment20231117_no_modification/guppy/pass/*.fastq > experiment20231117_no_modification/basecalled.fastq'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'f5c index -t 4 -d experiment20231117_no_modification/fast5 experiment20231117_no_modification/basecalled.fastq'
####docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'f5c eventalign -t 4 -r experiment20231117_no_modification/basecalled.fastq -b experiment20231117_no_modification/minimap.filt.sort.bam -g unmodified_all_all_all_rna_sequences_LYS.fasta --samples --print-read-names --scale-events --rna --disable-cuda=yes --min-mapq 0 | nanocompore eventalign_collapse -t 4 -o eventalign_collapse --log_level debug'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data wkusmirek/f5c:1.4 bash -c '/f5c/f5c eventalign -t 4 -r experiment20231117_no_modification/basecalled.fastq -b experiment20231117_no_modification/minimap.filt.sort.bam -g unmodified_all_all_all_rna_sequences_LYS.fasta --samples --print-read-names --scale-events --rna --min-mapq 0 --min-recalib-events 5 -o experiment20231117_no_modification/eventalign.sam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'nanocompore eventalign_collapse -t 4 --eventalign experiment20231117_no_modification/eventalign.sam -o experiment20231117_no_modification/eventalign_collapse --log_level debug'

==============================================
====== experiment20231120_ncm5SU_long =======
==============================================
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'minimap2 -x map-ont -t 4 -a unmodified_all_all_all_rna_sequences_LYS.fasta experiment20231120_ncm5SU_long/guppy/pass/*.fastq > experiment20231120_ncm5SU_long/minimap.sam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools view experiment20231120_ncm5SU_long/minimap.sam -bh -t unmodified_all_all_all_rna_sequences_LYS.fasta.fai -F 2324 | samtools sort -@ 4 -o experiment20231120_ncm5SU_long/minimap.filt.sort.bam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools index experiment20231120_ncm5SU_long/minimap.filt.sort.bam experiment20231120_ncm5SU_long/minimap.filt.sort.bam.bai'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'cat experiment20231120_ncm5SU_long/guppy/pass/*.fastq > experiment20231120_ncm5SU_long/basecalled.fastq'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'f5c index -t 4 -d experiment20231120_ncm5SU_long/fast5 experiment20231120_ncm5SU_long/basecalled.fastq'
####docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'f5c eventalign -t 4 -r experiment20231120_ncm5SU_long/basecalled.fastq -b experiment20231120_ncm5SU_long/minimap.filt.sort.bam -g unmodified_all_all_all_rna_sequences_LYS.fasta --samples --print-read-names --scale-events --rna --disable-cuda=yes --min-mapq 0 | nanocompore eventalign_collapse -t 4 -o eventalign_collapse --log_level debug'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data wkusmirek/f5c:1.4 bash -c '/f5c/f5c eventalign -t 4 -r experiment20231120_ncm5SU_long/basecalled.fastq -b experiment20231120_ncm5SU_long/minimap.filt.sort.bam -g unmodified_all_all_all_rna_sequences_LYS.fasta --samples --print-read-names --scale-events --rna --min-mapq 0 --min-recalib-events 5 -o experiment20231120_ncm5SU_long/eventalign.sam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'nanocompore eventalign_collapse -t 4 --eventalign experiment20231120_ncm5SU_long/eventalign.sam -o experiment20231120_ncm5SU_long/eventalign_collapse --log_level debug'

docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 bash -c 'nanocompore sampcomp --file_list1 experiment20231117_no_modification/eventalign_collapse/out_eventalign_collapse.tsv --file_list2 experiment20231120_ncm5SU_long/eventalign_collapse/out_eventalign_collapse.tsv --label1 Control --label2 Dataset --fasta unmodified_all_all_all_rna_sequences_LYS.fasta --outpath nanocompore_result --sequence_context 2 --downsample_high_coverage 5000 --allow_warnings --pvalue_thr 0.05 --min_coverage 1 --logit --nthreads 4 --log_level debug'

docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/nanocompore:v1.0.4 python3
from nanocompore.SampCompDB import SampCompDB, jhelp
import matplotlib.pyplot as pl
db = SampCompDB (db_fn = "nanocompore_result/outSampComp.db", fasta_fn = "unmodified_all_all_all_rna_sequences_LYS.fasta")
fig, ax = db.plot_pvalue ("ref")
fig.savefig('plot_pvalue')
fig, ax = db.plot_pvalue ("ref", palette="Set1")
fig.savefig('plot_pvalue_set1')
fig, ax = db.plot_signal ("ref", start=0, end=200)
fig.savefig('plot_signal')
fig, ax = db.plot_signal ("ref", start=0, end=200, kind="swarmplot")
fig.savefig('plot_signal_swarmplot')
fig, ax = db.plot_coverage ("ref")
fig.savefig('plot_coverage')
fig, ax = db.plot_kmers_stats ("ref")
fig.savefig('plot_kmers_stats')
#fig, ax = db.plot_position ("ref", pos=82)
#fig.savefig('plot_position')


=====================================
====== Nanopolish
=====================================

docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data nanozoo/nanopolish:0.13.2--9069b5c bash -c 'nanopolish index -d experiment20231120_ncm5SU_long/fast5 experiment20231120_ncm5SU_long/basecalled.fastq'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'minimap2 -ax map-ont -t 8 unmodified_all_all_all_rna_sequences_LYS.fasta experiment20231120_ncm5SU_long/basecalled.fastq | samtools sort -o experiment20231120_ncm5SU_long/reads-ref.sorted.bam -T reads.tmp'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools index experiment20231120_ncm5SU_long/reads-ref.sorted.bam'
docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data tleonardi/minimap2:2.17 bash -c 'samtools quickcheck experiment20231120_ncm5SU_long/reads-ref.sorted.bam'

docker run --rm -it -v /home/wiktor/nanocompore_pipeline/test_data:/home/wiktor/nanocompore_pipeline/test_data -w /home/wiktor/nanocompore_pipeline/test_data nanozoo/nanopolish:0.13.2--9069b5c bash -c 'nanopolish eventalign --reads experiment20231120_ncm5SU_long/basecalled.fastq --bam experiment20231120_ncm5SU_long/reads-ref.sorted.bam --genome unmodified_all_all_all_rna_sequences_LYS.fasta --scale-events > experiment20231120_ncm5SU_long/reads-ref.eventalign.txt'


# Nanocompore pipeline
This repo contains the code for running the [Nanocompore](https://github.com/tleonardi/nancompore) analysis workflow using [Nextflow](https://www.nextflow.io/).

## Pipeline steps
The pipeline runs the following steps:

* Basecalls the raw fast5 files using Guppy
* Run [pycoQC](https://github.com/a-slide/pycoQC) on Guppy's output
* (Optionally) Prepare a fasta file for the reference transcriptome from the genome fasta and transcriptome annotation in GTF
* Map the basecalled data to the reference using [minimap2](https://github.com/lh3/minimap2)
* Realign the raw signal-level data to the kmers of the reference with [f5c](https://github.com/hasindu2008/f5c)
* Collapse Nanopolish output by kmer using Nanocompore's eventalign_collapse
* Run Nanocompore

All steps are executed in a Docker/Singularity containers.

## How to run

### Sample annotation
Prepare a tab-separated file that describes the samples:
```
SampleName  Condition DataPath
WT1         WT        /path/to/fast5dir
WT2         WT        /path/to/fast5dir
KD1         KD        /path/to/fast5dir
KD2         KD        /path/to/fast5dir
```

### Configure the pipeline
Configure the pipeline by editing the _nextflow.config_ file.

All parameters are described in the comments and should be self explanatory.

The only two options that deserve an explanation are `target_trancripts` and `input_is_basecalled`.
The former allows you to provide the path to a text file that lists Ensembl transcript IDs of interest. 
Any transcript not present in this list will be discarded from the reference.
`input_is_basecalled` allows you to start the pipeline __after__ the Albacore step. In order for this to work,
the paths in the sample annotation file must point to basecalled fast5 files.

### Run the pipeline
To run the pipeline just execute:
`nextflow run pipeline.nf`

### Profiles
The pipeline is shipped with 3 profiles: local (default), lsf and aws_batch, which respectively run the processing on the local
machine, an LSF cluster or an AWS Batch computer environment.
The local profile limits the number of cuncurrent tasks to 10, which is reduced to 2 and 3 for Guppy and f5c respectively.
The LSF profile if configured to use dynamic memory management.
