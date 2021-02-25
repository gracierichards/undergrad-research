Command line BLAST generates text files as output. BLAST_to_Excel.py collects the data from these text files and organizes them into a table in an Excel spreadsheet. It creates a separate Excel file for each genus. Within each file are sheets for each species in the genus. It is formatted as a table with columns A through K. Column A has the sample name (basically the file that BLAST was run on) and column B indicates whether the sample tested positive or negative for Chlamydia. Column C has how many reads of that species were identified by the Kraken software, and column D has how many of those reads were confirmed to be that species by BLAST. Column E contains the first 4 BLAST hits for each read, unless the species is found. For example, if we are looking at Chlamydia trachomatis extracted reads, and Chlamydia trachomatis is the 6th hit in BLAST, then column E will list out the top 6 hits. Columns G and H, score and supported e-value respectively, list out these characteristics for each hit result. Columns F, I, and J, region/CDS, percent identity, and fraction identity respectively, summarize the information from the alignments section. Finally, column K has the length of the read.

Excel_Summary.py takes column C and D and puts them in a new file. The Excel file it creates is a table where each row is a sample, and each column is a species. The fractions represent the number of reads identified by Kraken (from column C of the other spreadsheet) over the number of reads confirmed by BLAST (from column D of the other spreadsheet).

Zoonotic_Excel.py performs the same function as BLAST_to_Excel.py. The difference is that BLAST_to_Excel.py is given a directory (e.g. called Chlamydia_trachomatis/) and it loops through all of the files inside (e.g. called 30C_blasted.txt). Zoonotic_Excel.py is given a genus instead of a species directory, and the files inside consist of many species and samples (e.g. 107V_Brucella_abortus.txt, 30R_Brucella_melitensis.txt).

Zoonotic_Summary.py is a work in progress.

GR_extraction extracts all reads (that are species or subspecies level) from a sequence file according to the classification done by Kraken. It should be run in a directory, and afterwards will create subdirectories for each category of pathogens. For each species, all sequences of that species are saved in a file in the correct category. GR_extraction_FASTA.py should be used if BLAST is downstream in your workflow. It takes FASTQ files as input; it's named FASTA because it outputs FASTA format. If you want to save sequences with their quality scores, use GR_extraction_FASTQ.py.

Usage is
>python GR_extraction_FASTA.py sample_name

where sample_name is a prefix of your file name like 30C.
