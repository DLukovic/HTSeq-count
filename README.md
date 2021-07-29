# HTSeq-count
Given a file with aligned sequencing reads (sorted.bam) and a list of genomic features, a common task is to count how many reads map to each feature.

In the case of RNA-Seq, the features are typically genes, where each gene is considered here as the union of all its exons. One may also consider each exon as a feature, e.g., in order to check for alternative splicing. 

RUN following HTSeq-Count script with python3:

		Python3 Version 3.9
		HTSeq-Count Version 0.11.1
		annotation gtf file downloaded from Ensembl SScrofa11.1-> genes.gtf
		
		$ python3 -m HTSeq.scripts.count -f bam -r pos -t exon --additional-attr=gene_name stranded=reverse 		15618Aligned.sortedByCoord.out.bam genes.gtf > 15618.counts
		
RUN the script on all samples using loop:

		cd path/to/samples
		./htseq-bash-loop.sh
		
		#!/bin/bash

		many_files=$(find /Users/domilukovic/Desktop/htseq-test -name "*.bam")
		echo $many_files

		gtf_file=$(find 		/Users/domilukovic/Projects/Fibrosis_Project/Ref_Genomes_Sscrofa11.1/Ensembl/Sus_scrofa_Ensembl_Sscrofa11.1/Sus_scrofa/Ensembl/Sscrof		a11.1/Annotation/Archives/archive-2018-04-12-14-32-18/Genes -name "*.gtf")
		echo $gtf_file

		for one_file in $many_files; do
	
		echo "HTseq-count of $one_file"

		python3 -m HTSeq.scripts.count -f bam -r pos -t exon -s reverse --additional-attr=gene_name $one_file $gtf_file  > $one_file.count

		done
		
