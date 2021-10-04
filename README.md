## How to convert 10X original BAM to FASTQ

### References
- `bamtofastq`
    - https://support.10xgenomics.com/docs/bamtofastq
    - https://github.com/10XGenomics/bamtofastq
    - https://github.com/10XGenomics/bamtofastq/releases
    - https://github.com/10XGenomics/bamtofastq/issues/22
- SRA toolkit
    - https://github.com/ncbi/sra-tools
    - https://hpc.nih.gov/apps/sratoolkit.html
- ETC
    - https://bioinformatics.stackexchange.com/questions/7096/bam-to-gene-expression-matrix-umi-counts-per-gene-per-cell-10x

### Note
- This conversion is only available when the BAM file is produced by 10X cellranger
- When using NCBI SRA, check out whether a given SRA provides an **original format BAM file** (see bottom of the data access page)

### Getting an input BAM file downloaded from NCBI SRA

- Option 1: using **wget <BAM file location>**

```bash
wget https://sra-download.ncbi.nlm.nih.gov/traces/sra38/SRZ/011947/SRR11947587/10X25_4_A_1.bam
```


- Option 2: using **prefetch <SRA accession number>** (from SRA toolkit)

```bash
prefetch --type TenX --max-size 100000000 SRR11947587

# If the file is larger than the default limit of 20GB,
# Set the flag --max-size
```


### Getting `bamtofastq` installed

- The the newest version from [10x GitHub repo](https://github.com/10XGenomics/bamtofastq/releases/)
- Note: bamtofastq is a single executable that can be run directly and requires no compilation or installation. Place the executable file in a directory that is on your PATH, and make sure to chmod 700 to make it executable.

```bash

# File download
wget https://github.com/10XGenomics/bamtofastq/releases/download/v1.3.5/bamtofastq_linux

# Check out the file and commands
./bamtofastq_linux --help

# Make the file executable
chmod 700 bamtofastq_linux
```


### Converting BAM to FASTQ

- Run `bamtofastq` (interactive session required if needed)

```bash
./bamtofastq nthreads=8 test.bam
```


