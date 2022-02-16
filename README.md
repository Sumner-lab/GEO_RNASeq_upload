# GEO_RNASeq_upload

This page is to simplify the upload of data to GEO (Gene Expression Omnibus), which is the portal in which you can upload raw reads and gene expression counts to NCBI.

Uploading counts and expression data is the standard procedure for RNA-Seq experiments, although if you wish not to upload expression counts (so, only raw counts), then you have to upload raw reads directly through SRA (Sequence read archive, on NCBI) and not GEO.

If you used a public genome and annotation, continue to next steps. If not, then we need to upload the genome and assembly to NCBI first (*We need a page to explain this too*)

Steps to upload the data.

1. Make sure you are logged on to the VPN CISCO AnyConnect (if you are outside UCL).
2. Make an expression counts table, these could be from featureCounts (e.g. Nextflow rnaseq pipeline). You can submit these per sample, or provide a single table (in the example I submit a single counts table).

3. Make sure all your raw reads and expression count files are in the same folder. 
For me I had to link all my files in a new directory:
#copying the raw data links to a single folder:
`ln -s /Volumes/ritd-ag-project-rd016y-eefav92/Polybia_occidentalis/experiment2/data/*/raw/*.gz .`
#copying my counts table into same folder:
`cp /Volumes/ritd-ag-project-rd016y-eefav92/Polybia_occidentalis/experiment2/NCBI_counts_table.txt .`

4. Copy the excel table in this repo (Multispecies...), which provides a basic template to upload your data.
5. Start filling in the basic details of the project (see document, and examples 1 and 2 for more info). 
e.g.:
title
summary
overall design

HINT: If you hover over the cell titles, it will give you further information about the data type or expected input.

6. Work out the length of your reads (Either check manually, ask sequencing facility or use FASTQC [within nextflow rnaseq run])
7. Work out Illumina machine name (ask sequencing facility).
8. Add custom characteristics columns with useful features, such as caste (in the example)
9. **Processed data**. 
10. First you need to enter the annotation you used from NCBI. Under genome (see Example 1 tab). If you do not have a genome, remove line.
11. Add data processing steps, to explain briefly what programs were run on the data to get the processed file/s.
12. Add final processed file format and content info.
13. **Raw files ** 
14. Add sample raw file names, data type.
15. Add the md5 sums. These are unique hash codes for a particular file. This ensures that the files are copied correctly to the NCBI database.

On mac you use md5 and on linux (inc cluster) you use md5sum . These are standard terminal commands, and require you to specify the files you want hashes for. 
`md5 *.gz`

E.g. in the above example, on a macm, giev me the hashes for all files in the current directory with the ending .gz. 

WANRING: This may take >30mins or more, deopending on file sizes and number.

9. Copy this md5 table into the excel spreadsheet where it has md5 as a header of the section. Match them up to your dataset by sorting the rows alphabetically.
10. 
