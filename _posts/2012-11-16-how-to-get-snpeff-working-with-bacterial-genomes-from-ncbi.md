---
layout: post
title: "How to get snpEff working with bacterial genomes from NCBI"
description: ""
category: notebook 
tags: []
---


You can do this from GFF files. You need the GFF file and corresponding FNA file. 

Create a nickname

	<databasename>

and add to "genomes" list at top of snpEff.config.

Add a line at the bottom of snpEff.config:

	<databasename>.genome : Descriptive Name

The FNA should be renamed and the header line rewritten to match the GFF header:

	data/genomes/<databasename>.fa

The GFF file should go in:

	data/<databasename>/genes.gff

Then build the database:

	java -jar bin/snpEff_2_0_5d/snpEff.jar build -gff3 -v <databasename>

Ensure the snpEff.config has the bacterial codon table selected:

	<databasename>.genome : <description>
        	<databasename>.chromosomes : <fastahdrid>
        	<databasename>.<fastahdrid>.: Bacterial_and_Plant_Plastid

The VCF file also needs to match the modified header

Then:

	java -jar bin/snpEff_2_0_5d/snpEff.jar eff -no-downstream -no-upstream -no-utr -no-intergenic -o vcf -c snpEff.config <databasename> vcffile



