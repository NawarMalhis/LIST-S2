# LIST-S2
LIST-S2: Taxonomy based sorting of pathogenic missense mutations across species

LIST-S2 generates Position Conservation Matrixes for protein sequences in fasta format.
- First, input sequences are aligned to the UniProt Swiss-Prot/TrEMBL
- Then, it computes a deleteriousness value for every possible AA mutation in the sequence based on the LIST-S2 algorithm.

Minimum hardware requirement:
Ubuntu platform running on a desktop computer with at least 16G RAM, and a 4 cores CPU. Disk IO is the main performance bottleneck, thus SSD is recommended.

To install and test LIST-S2

1: Install the blast alignment tools, please type:
     sudo apt-get install ncbi-blast+
2: Unpack the LIST-S2.tar.gz file.
3: from: https://www.uniprot.org/downloads/ Download into the UniProt directory:
     Reviewed (Swiss-Prot) fasta and
     Unreviewed (TrEMBL) fasta
4: from: ftp://ftp.ncbi.nlm.nih.gov/pub/taxonomy/ Download into the Taxa directory:
     taxdump.tar.gz
5: Compile source code, please type:
     make
6: Unpack and format downloaded data files, type
     make unpack               (processing time is 1~3 hours)

To run the test sequences in the data directory, please type:
./list-s2 data

Running LIST-S2
LIST-S2 processes all fasta sequences in the target directory. Each sequence must be in a fasta format in a separate file with the extension ‘.fast’.
The UniProt database is divided into 33 equal sections. Each input sequence is aligned to all 33 sections, and then results are merged. LIST-S2 utilize system memory caching to reduce disk read by aligning up to n (default n=100) sequences to each of the DB 33 sections before start aligning to the next section. 

NCBI blastp is used for alignment using m threads (default m = 4). To use different n and m values, include these values in the command line:
./list-s2 dataDir [n m]
Note that dataDir needs to be inside the current directory.

Example:
./list-s2 data 5 6
Process all sequences in the data directory, 5 sequences are aligned for each DB read using 6 threads.
