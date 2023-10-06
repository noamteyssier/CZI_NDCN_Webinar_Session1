# CZI_NDCN_Webinar_Session1

The results of the workshop and example data from CZI NDCN Webinar Session 1

If you'd like to see more please check out my [How Do I...?](https://noamteyssier.github.io/howdoi/crispr_screen/intro.html)
Series.

## Workflow

### Input Data

The input data for this can be downloaded from the following link: <http://u.pc.cd/3UV>

It is a `TAR` archive and can be decompressed like so:

```bash
tar -xzvf sequences.tar.gz
```

This will create a new directory called `sequences` that will be populated with
the sequencing files.

### sgRNA Counts Mapping

The command used for mapping counts is [`sgcount`](https://noamteyssier.github.io/sgcount/).

``` bash
sgcount \
    -l meta/h5_lib.var.fa \
    -g meta/h5_lib.g2s.txt \
    -i \
        sequences/ctrl_1.fastq.gz \
        sequences/ctrl_2.fastq.gz \
        sequences/ctrl_3.fastq.gz \
        sequences/test_1.fastq.gz \
        sequences/test_2.fastq.gz \
        sequences/test_3.fastq.gz \
    -n \
        ctrl_1 \
        ctrl_2 \
        ctrl_3 \
        test_1 \
        test_2 \
        test_3 \
    -t 6 \
    -o results/mapping.tsv
```

### Differential Abundance + Gene Aggregation

The command used for differential abundance testing and gene aggregation
is [`crispr_screen`](https://noamteyssier.github.io/crispr_screen/).

```bash
crispr_screen \
    -i results/mapping.tsv \
    -c ctrl_1 ctrl_2 ctrl_3 \
    -t test_1 test_2 test_3 \
    -o results/results
```

### Screen Visualization

The command used to generate volcano plots for genes and sgRNAs is
[`screenviz`](https://github.com/noamteyssier/screenviz).

``` bash
screenviz gene \
    -i results/results.gene_results.tsv \
    -o figures/gene_volcano.html

screenviz sgrna \
    -i results/results.sgrna_results.tsv \
    -o figures/sgrna_volcano.html
```

### IDEA Analysis

A jupyter notebook for the IDEA analysis can be viewed in `notebooks/IDEA.ipynb`.
