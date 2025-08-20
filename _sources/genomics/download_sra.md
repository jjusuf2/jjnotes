# Download raw sequencing data

Need to download raw high-throughput sequencing data from a published paper? Most raw data is shared on the NCBI [Sequence Read Archive](https://www.ncbi.nlm.nih.gov/sra) (SRA). To download raw data, you will need to install a software package called [SRA toolkit](https://github.com/ncbi/sra-tools).

In this example, we will download raw data from a Micro-C experiment from Hsieh et al. 2020 (GEO: [GSE130275](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE130275)). Let's download the raw data for the Micro-C on wild-type mESCs, replicate 1 ("ESC_WT01"). Its SRA accession number is SRR8954797, which can be found at the bottom of the dataset's GEO entry.

> **_NOTE:_** Sometimes, one sequencing experiment can be split across multiple SRA accession numbers. In this case, you will have to download them individually and merge them later.

First, run the following command (replacing the path to the _sratoolkit_ folder and version number if necessary):
```
export PATH=$PATH:~/sratoolkit.3.0.10-ubuntu64/bin
```

Then, navigate to the directory where you want to download the data, and run the following command:
```
prefetch -v --max-size u SRR8954797
```
The option `--max-size u` removes any preexisting limits on the maximum size of the downloaded file.

Then, run the following command:
```
fasterq-dump --split-files SRR8954797
```

Since this is a paired-end experiment, we use the `--split-files` flag, resulting in two files: `SRR8954797_1.fastq` and `SRR8954797_2.fastq`. Note that some additional flags typically used in the older command `fastq-dump` are no longer needed; `fasterq-dump` automatically skips technical reads, applies appropriate filters, and compresses the output.

Lastly, compress the files, if desired:
```
gzip SRR8954797_1.fastq & gzip SRR8954797_2.fastq
```