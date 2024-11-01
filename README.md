# TOSMuVar
TOSMuvar is tailored for the detection of somatic variants in tumor only samples using long-read sequencing data from Oxford Nanopore technology, employing ClairS-TO for variant calling to enhance accuracy and resolution in identifying complex genomic alterations.

# Getting Started
**Prerequisites** :

Docker  
Python  
R  

  **Variant Caller**  
-  ClairS-TO (https://github.com/HKU-BAL/ClairS-TO)

   ClairS-TO (Somatic Tumor-Only) is a tool in the Clair series to support long-read somatic small variant calling with only tumor samples available.
   
   **Installation** :  
   docker pull hkubal/clairs-to

**Other tools**

- Nanoplot (https://github.com/wdecoster/NanoPlot)
- Porechop (https://github.com/rrwick/Porechop)  
- Minimap2 (https://github.com/lh3/minimap2)
- Samtools (https://github.com/samtools/samtools) 
- BCFtools (https://samtools.github.io/bcftools/howtos/index.html)

# Overview of the Pipeline  

The TOSMuVar.sh  script is designed for efficient genomic analysis with several key features:  

**1) Input Parameters** : The script accepts several command-line options for configuration, including:
- -w Specifies the working directory
- -r Reference genome file (hg38.fasta with its index file, it has to be in the Clairs-To variant caller folder)
- -b BED file for region of interest
    
**2) Docker Permissions Check** : The script checks Docker accessibility and prompts for sudo credentials if permissions on the Docker socket need to be fixed.  

**3) Quality Control with NanoPlot** : It identifies FASTQ files in the specified directory and generates quality plots using NanoPlot for initial data assessment.

**4) Trimming with Porechop** : Barcodes are removed from the FASTQ files to ensure clean data for alignment.  

**5) Alignment with Minimap2** : The trimmed FASTQ files are aligned to the reference genome, producing SAM files for further processing.  

**6) Sorting and Indexing** : SAM files are converted to sorted BAM format using samtools, followed by indexing to facilitate efficient data retrieval.  

**7) Coverage and Depth Analysis** : The script computes coverage statistics for specified regions based on the BED file and generates depth information for each BAM file.

**8) SNP Calling with ClairS-TO** : Utilizing Docker, the ClairS-TO pipeline is run for variant calling on each sorted BAM file, enabling comprehensive SNP detection.  

**9)  VCF to CSV Conversion** : The resulting VCF files from ClairS-TO are converted into a user-friendly CSV format for easier analysis.  

**10) SNP Plotting** : It plots VAF and RAF against their positions, offering a clear visual representation of allele frequencies across the genome to analyze the trand for potential LOH.
       
 






