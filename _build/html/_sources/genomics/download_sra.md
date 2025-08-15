# Download SRA

The NCBI Sequence Read Archive (SRA) is an online repository of raw data from high-throughput sequencing experiments. To download raw data, you must obtain the accession number (SRR...) of the dataset you are interested in. You will also need to download the [SRA toolkit](https://github.com/ncbi/sra-tools).

First, run this command from the home directory (replacing the version number if necessary):
```
export PATH=$PATH:$PWD/sratoolkit.3.0.10-ubuntu64/bin
```

Then, in the directory where you want to download the data, run the following command (replacing the SRR number with the appropriate one):
```
prefetch -v --max-size u SRR31974205
```



Lastly, run the following command (replacing the SRR number):
```
fastq-dump --outdir /path/to/output/directory --dumpbase --skip-technical --clip --read-filter pass --gzip SRR31974205
```