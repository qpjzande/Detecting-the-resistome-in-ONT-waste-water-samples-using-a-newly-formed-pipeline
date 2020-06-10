# Detecting-the-resistome-in-ONT-waste-water-samples-using-a-newly-formed-pipeline
In this research, we developed a pipeline to detect antibiotic resistance genes in ONT data

**Goal:**\
The goal of this project is to develop a pipeline that is able to detect antibiotic resistance genes in metagenomic samples and give a overall overview of what resistance genes are present in used datasets.

ONT data is used to develop the pipeline, Illumina data is used as a control whether the pipeline produces reliable output.

**Flowchart:**

![](images/flowchart%20end.jpg)/


**Used datasets:**\
gridION:\
*AWGS180032_LR (2.7 Gb)*\
*AWGS180033_LR (6.2 Gb)*

HiSeq paired (duplicates as control):\
*SR32_SR_1.fastq (452 Mb)*\
*SR32_SR_2.fastq (479 Mb)*\
*SR33_SR_1.fastq (404 Mb)*\
*SR33_SR_2.fastq (428 Mb)*\
\
**Below are the steps used in this project:**

Step1:
upload the data to Galaxy (http://galaxy.bioinformatics-atgm.nl:2222/)

Step2:
Run nanoplot on long read data and filter the data using filtlong (min. mean quality = 90, min. read length = 1000)

Step3:
download the filtered files and upload them into Linux (lisa.surfsara.nl).

Step3:
Download the Resfinder database from https://cge.cbs.dtu.dk/services/ResFinder/ and upload the files to Linux. Then, use CAT to create one merged file.

Step4:
Run KMA on both filtered long read files using the Resfinder database as template. Download the .res output files and open them in Microsoft Excel.

Step5:
Back in Galaxy, run FastQC on Illumina data and trim the first 15 nucleotides using trimmomatic's Headcrop feature.

Step6:
Assemble the trimmed reads using Shovill on default settings.

Step7:
Run Staramr on both assemblies, with the Pointfinder database disabled.

Step8:
Compare the data of the duplicates analyzed using both Oxford Nanopore and Illumina technologies,

Step9:
To simplify the database, Find out for each subgroup which subtype has the highest identity value. All other subtypes within this group are removed from the database. This is done for all detected groups within the datasets.

\
**To install KMA in linux:**\
installation:\
*conda install kma*

activation:\
*conda activate ENVIRONMENT*

\
**To run KMA in linux:**

Create a database index using the following command:\
*kma index -i DATABASE_FILE -o OUTPUT_NAME*

Run KMA:\
*kma -i INPUT_FILE -o OUTPUT_FILE -t_db INDEXED_DATABASE*

\
**Files within repository:**

Simplified database (only the detected genes were simplified): *Database32final1.fasta*\
Output from genomic ONT dataset AWGS180032_LR: *output_32.1f.res*\
Output from genomic ONT dataset AWGS180033_LR: *output_33.f1.res*\
Output from metagenomic ONT dataset barcode5: *output_05.f.res*\
Output from metagenomic ONT dataset barcode06: *output_06.f1.res*\
Output from genomic Illumina dataset SR_32: 
Output from genomic Illumina dataset SR_33: 
