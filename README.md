# LIST-S2
LIST-S2: Taxonomy based sorting of pathogenic missense mutations across species

## About
LIST-S2 generates Position Conservation Matrixes for protein sequences in fasta format.
- First, input sequences are aligned to the UniProt Swiss-Prot/TrEMBL
- Then, it computes a deleteriousness value for every possible AA mutation in the sequence based on the LIST-S2 algorithm.

#### Please reference the following publications:

Malhis N, Jacobson M, Jones SJM, Gsponer J. LIST-S2: taxonomy based sorting of deleterious missense mutations across species. *Nucleic Acids Research* (2020). [doi:10.1093/nar/gkaa288.](https://doi.org/10.1093/nar/gkaa288) 

Malhis N, Jones SJM, Gsponer J. Improved measures for evolutionary conservation that exploit taxonomy distances. *Nature Communications* (2019) Apr 5;10(1):1556. [doi:10.1038/s41467-019-09583-2.](https://www.nature.com/articles/s41467-019-09583-2) [pmid:30952844.](https://pubmed.ncbi.nlm.nih.gov/30952844/)
## Minimum Hardware Requirements

OS: Linux (tested on Ubuntu and CentOS7)

RAM: 8G minimum, 16G recommended

CPU: Multicore with 4+ cores recommended.

Disk: Disk IO is the main performance bottleneck, thus an SSD is recommended.

## Installation

### To install LIST-S2 v1.10

1. Install the blast alignment tools:
```bash
sudo apt-get install ncbi-blast+
```
2. Unpack the LIST-S2_v1.10.tar.gz file:
```bash
tar -xzvf LIST-S2.tar.gz
```
3. Compile source code:
```bash
make
```
4. Download UniProt 2019_02 Swiss-Prot and TrEMBL formated database (should take ~1 hour):
```bash
make database
```

### To install LIST-S2 (V1)

1. Install the blast alignment tools:
```bash
sudo apt-get install ncbi-blast+
```
2. Unpack the LIST-S2.tar.gz file:
```bash
tar -xzvf LIST-S2.tar.gz
```
3. Download 'Reviewed (Swiss-Prot) fasta' and 'Unreviewed (TrEMBL) fasta' from the [Uniprot downloads page](https://www.uniprot.org/downloads) into the UniProt directory:
```bash
wget ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_sprot.fasta.gz
wget ftp://ftp.uniprot.org/pub/databases/uniprot/current_release/knowledgebase/complete/uniprot_trembl.fasta.gz
```  
4. Download 'taxdump.tar.gz' from the [NCBI taxonomy ftp](//ftp.ncbi.nlm.nih.gov/pub/taxonomy) into the Taxa directory"
```bash
wget ftp://ftp.ncbi.nlm.nih.gov/pub/taxonomy/taxdump.tar.gz
```
5. Compile source code:
```bash
make
```
6. Unpack and format downloaded data files (processing time is 1~3 hours):
```bash
make unpack
```

## Running LIST-S2

To run the test sequences in the `data` directory:
```bash
./list-s2 data
```

LIST-S2 processes all fasta sequences in the target directory. Each sequence must be in a fasta format in a separate file with the extension ‘.fasta’.
The UniProt database is divided into 33 equal sections. Each input sequence is aligned to all 33 sections, and then results are merged. LIST-S2 utilizes system memory caching to reduce disk read by aligning up to n (default n=100) sequences to each of the DBs 33 sections before starting aligning to the next section. 

NCBI blastp is used for alignment using m threads (default m = 4). To use different n and m values, include these values in the command line:
```bash
./list-s2 dataDir [n m]
```
Note: that dataDir needs to be inside the current directory.

Example: Process all sequences in the data directory, 5 sequences are aligned for each DB read using 6 threads.
```bash
./list-s2 data 5 6
```

# LIST-S2 Webtool Source Code

## Processing Queue
Source Code: https://github.com/JacobsonMT/CCRS

## HTML Interface
Link: https://list-s2.msl.ubc.ca/

Source Code: https://github.com/JacobsonMT/CCRS-html-client

## REST API
Link: https://list-s2-api.msl.ubc.ca/

Source Code: https://github.com/JacobsonMT/CCRS-html-client/tree/api

## Precomputed Predictions
Link: https://precomputed.list-s2.msl.ubc.ca/

Source Code: https://github.com/JacobsonMT/PolyST/tree/multi-species
