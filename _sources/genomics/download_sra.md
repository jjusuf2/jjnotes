# Download raw data from SRA

Need to download raw high-throughput sequencing data from a published paper? Most raw data is shared on the NCBI [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA). First, you must find the accession number (SRR...) of the dataset you are interested in, which is usually at the bottom of the dataset's GEO entry. A single biological sample can have one SRR number or be split across multiple.

You will also need to download a software package called [SRA toolkit](https://github.com/ncbi/sra-tools).

First, run the following command (replacing the path to the folder and version number if necessary):
```
export PATH=$PATH:<path/to/sratoolkit.3.0.10-ubuntu64/bin>
```

Then, navigate to the directory where you want to download the data, and run the following command, replacing the SRR number as necessary:
```
prefetch -v --max-size u <SRR_number>
```
The option `--max-size u` removes any existing limits on the maximum size of the downloaded file.

Then, run the following command, replacing the SRR number as necessary:
```
fasterq-dump --outdir </path/to/output/directory> --split-files <SRR_number>
```

The `--split-files` flag creates two files, `<SRR_number>_1.fastq` and `<SRR_number>_2.fastq`. Note that some additional flags typically used in the older command `fastq-dump` are no longer needed; `fasterq-dump` automatically skips technical reads, applies appropriate filters, and compresses the output.

Lastly, compress the files, if desired:
```
gzip <SRR_number>_1.fastq & gzip <SRR_number>_2.fastq
```