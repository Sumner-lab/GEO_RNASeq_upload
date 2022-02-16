# GEO_RNASeq_upload

This page is to simplify the upload of data to GEO (Gene Expression Omnibus), which is the portal in which you can upload raw reads and gene expression counts to NCBI.

Uploading counts and expression data is the standard procedure for RNA-Seq experiments, although if you wish not to upload expression counts (so, only raw counts), then you have to upload raw reads directly through SRA (Sequence read archive, on NCBI) and not GEO.

If you used a public genome and annotation, continue to next steps. If not, then we need to upload the genome and assembly to NCBI first (*We need a page to explain this too*)


**Prerequisites:**
1. Make sure you are logged on to the VPN CISCO AnyConnect (if you are outside UCL).
2. Make an account with NCBI: https://www.ncbi.nlm.nih.gov/geo/
3. Download Filezila client. https://filezilla-project.org/ 

**Compile data**
4. Make an expression counts table, these could be from featureCounts (e.g. Nextflow rnaseq pipeline). You can submit these per sample, or provide a single table (in the example I submit a single counts table).
5. Make sure all your raw reads and expression count files are in the same folder. 
For me I had to link all my files in a new directory:
#copying the raw data links to a single folder:
`ln -s /Volumes/ritd-ag-project-rd016y-eefav92/Polybia_occidentalis/experiment2/data/*/raw/*.gz .`
#copying my counts table into same folder:
`cp /Volumes/ritd-ag-project-rd016y-eefav92/Polybia_occidentalis/experiment2/NCBI_counts_table.txt .`
6. Copy the excel table in this repo (Multispecies...), which provides a basic template to upload your data.

**Fill in excel spreadsheet**
7. Start filling in the basic details of the project (see document, and examples 1 and 2 for more info). 
e.g.:
title
summary
overall design

HINT: If you hover over the cell titles, it will give you further information about the data type or expected input.

8. Work out the length of your reads (Either check manually, ask sequencing facility or use FASTQC [within nextflow rnaseq run])
9. Work out Illumina machine name (ask sequencing facility).
10. Add custom characteristics columns with useful features, such as caste (in the example)
 
**Processed data**. 
11. First you need to enter the annotation you used from NCBI. Under genome (see Example 1 tab). If you do not have a genome, remove line.
12. Add data processing steps, to explain briefly what programs were run on the data to get the processed file/s.
13. Add final processed file format and content info.

**Raw files ** 
14. Add sample raw file names, data type.
15. Add the md5 sums. These are unique hash codes for a particular file. This ensures that the files are copied correctly to the NCBI database.

On mac you use md5 and on linux (inc cluster) you use md5sum . These are standard terminal commands, and require you to specify the files you want hashes for. 
`md5 *.gz`

E.g. in the above example, on a macm, giev me the hashes for all files in the current directory with the ending .gz. 

WANRING: This may take >30mins or more, deopending on file sizes and number.

16. Copy this md5 table into the excel spreadsheet where it has md5 as a header of the section. Match them up to your dataset by sorting the rows alphabetically.
17. Add: instrument model, read length, single or paired-end
18. Put in paired end data at end of excel table, paired R1 then R2. If your data are single end, leave this section blank.

**Submission to NCBI**
19. Go to https://www.ncbi.nlm.nih.gov/geo/ and login. Go to https://www.ncbi.nlm.nih.gov/geo/info/seq.html and click "Transfer files"
20. Follow their instructions for filezila: https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html
21. ONce you are connected to their server, you need to find your folder with data in it on the left (normally). Then select the files you want to transfer, and drag and drop them over to the server side in a folder with an appropriate name (e.g. Polybia_GEO_Submission). 
WARNING: This step could take >24hours, esp. if the data are on the RDS, which is super slow moving files. If the copy breaks, you can always try again later, and move the files that didn't transfer correctly.

22. Once the files have all been transferred (excel table, raw counts, and gene expression), go back to GEO, and select "notify GEO". Follow their instructions, including choosing a publish date. This is provisional, but you can put three years from now, and can always remove the data if your paper is not ready by then.
