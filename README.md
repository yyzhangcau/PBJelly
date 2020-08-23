# PBJelly
# PBSuite_15.8.24
***A fork of the gap-closing pipeline PBJelly, not official.*** 
***All updates here are for in-house using and no warranty.***
Official Download address: https://sourceforge.net/projects/pb-jelly/
Part of the PBSuite of applications including PB Honey(https://www.hgsc.bcm.edu/software/honey).

## Requirements
- python 2.7
- networkx 1.7
- blasr 5.3.3
- boost/1.73.0
- hdf/1.8.21

## Installation
Using a conda enviroment.
```bash
module load boost/1.73.0
module load hdf5/1.8.21

conda create -n pbjelly
conda activate pbjelly
conda install python=2.7
pip install networkx=1.7
conda install -c bioconda blasr=5.3.3
git clone https://github.com/geneticswithme/PBJelly
```
Edit setup.sh and change `$WHERE_is_DIR_PBSuite_15.8.24` to the FULL DIRECTORY where the package `PBSuite_15.8.24` you've placed. 
```bash
source $WHERE_is_DIR_PBSuite_15.8.24/setup.sh
Jelly.py -h
```
## Usage
Example Protocol.xml:
```xml
<jellyProtocol>
    <reference>/FULL/PATH/TO/genome.fasta</reference>
    <outputDir>/FULL/PATH/TO/PBJellyOutputDIR/</outputDir>
    <blasr>--minMatch 8 --sdpTupleSize 8 --minPctIdentity 75 --bestn 1 --nCandidates 10 --maxScore -500 --nproc 8 --noSplitSubreads</blasr>
    <input baseDir="/FULL/PATH/TO/dataDIR/">
        <job>pacbioReads.fasta</job>
    </input>
</jellyProtocol>
```

```bash
cd PBJelly/docs/jellyExample
# Edit your Protocol.xml 
Jelly.py setup Protocol.xml
Jelly.py mapping Protocol.xml
Jelly.py support Protocol.xml
Jelly.py extraction Protocol.xml
Jelly.py assembly Protocol.xml 
Jelly.py output Protocol.xml
```
## Note
- Input sequences files must be end with ".fasta" or ".fastq"
- In Protocol.xml file, blasr options start with "--", not "-"
- The official PBSuite would stop at "mapping step", with "Error:No such file or directory:******fastq.m4". Updates here fixed this problem by changing the blasr argument from the "-" to "--".  