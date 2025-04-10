---
layout: post
title: Step-by-step tutorial to construct haplotype networks with PopArt
subtitle: Bioinformatics diaries No. 2 
show-avatar: false
tags: [bioinformatics]
permalink: /2024/09/30/haplotype-network
---

In our recent [bioRxiv pre-print](https://www.biorxiv.org/content/10.1101/2024.09.26.615256v1.abstract), we drew inspiration from a [previous study](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1001157) to use haplotype networks to investigate signatures of balancing selection in the duplicated human gene, _CD8B_.

To construct the network, I chose the software [PopArt](https://besjournals.onlinelibrary.wiley.com/doi/10.1111/2041-210X.12410) (Population Analysis with Reticulate Trees) due to its support for reticulations and availability on MacOS. The process was not entirely straightforward, so I decided to create a step-by-step tutorial—both for my own reference and to help others.

Shout-out to [this video](https://www.youtube.com/watch?v=7yQ5N9fpTSA) for helping me figure out key steps.

# Step 1: Generate a FASTA file of with sequences

First, generate a file with all the haplotype sequences you want to include in the network in FASTA format, where each haplotype is its own sequence:

```
>sample_X.hap1
ATCGGACGTTTACGAAAATCG...
>sample_X.hap2
ATCGGACGTGAACGAACCTCG...
>sample_Y.hap1
ATCGGACGTGTACGAAAATCG...
>sample_Y.hap2
ATCGGACGTGTACGAAGATCA...
```

_**Using fully-phased genome assemblies**_

If you are starting from fully-phased genome assemblies, you will need to map your assemblies to the reference genome and extract the nucleotide sequence of your locus of interest using `samtools consensus`. Here is how to do this.

First, map each haplotype to the reference genome using `minimap2` (or your favorite assembly-to-assembly aligner):

```bash
# map sequences in SAM format and convert to BAM
minimap2 -a --eqx --cs -x asm5 --secondary=no -s 25000 -K 8G reference.fa hap.fa | samtools view -Sb | samtools sort > hap.bam

# index alignment
samtools index hap.bam
```

Then, generate a file in FASTA format of the region of interest for each haplotype:

```bash
samtools consensus -m simple -r chrom:start-end -f fasta hap.bam > hap.locus.fa
```

Where `chrom:start-end` corresponds to the coordinates of the locus of interest.

Finally, merge all haplotype sequences for the locus of interest into a single FASTA file:

```bash
cat *.locus.fa > network_locus.fa
```

# Step 2: Align nucleotide sequences

Once nucleotide sequences are in a single FASTA file, we need to align them using a multiple DNA sequence alignment algorithm. There are multiple options for this, but I like to use MUSCLE software, which can be run from the command line, web applications, or desktop applications. Here I will show you how to run it in the desktop application.

First, you need to download and install MEGA software from their [official website](https://www.megasoftware.net/). After you have installed it, follow these steps.

First, load your FASTA file in the software, called `network_locus.fa` in this tutorial. Go to File > Open A File/Session and select "Align" in the pop-up window. The file nucleotide sequences will be displayed on the screen as follows:

![SS1](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS1.png?raw=true)

Sequences need to be aligned using the MUSCLE algorithm. Press the muscle icon on the menu and select "Align DNA". A pop-up window will ask if you want to select all sequences. Say "OK".

![SS2](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS2.png?raw=true)

Now you need to select the parameters for the MUSCLE alignment. I recommend using the defaults unless you have a good reason to change the parameters. The only parameter I change to make the process faster is the number of "Max Iterations". According to [MUSCLE user guide](https://www.drive5.com/muscle/muscle.html), running the two first iterations of the algorithm is "a good compromise between speed and accuracy."

![SS3](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS3.png?raw=true)

After the MUSCLE process is done, export the alignment file in **NEXUS format**, going to Data > Export Alignment > NEXUS/PAUP format.

![SS4](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS4.png?raw=true)

# Step 3: Add trait information

The trickiest part of building the network was to figure out how to display the sample ancestry and/or trait information. Thank you to Engy T. Megahed's for answering this question in [this thread](https://www.researchgate.net/post/How-to-insert-traits-and-coordinates-in-PopART).

The trait information needs to be manually added to the NEXUS file. Open the NEXUS file in any text editor.

The NEXUS file will have the following structure:
```
#NEXUS
[ TITLE ]
BEGIN TAXA;
       DIMENSIONS NTAX=4;
       TAXLABELS
             Sample_X.hap1
             Sample_X.hap2
             Sample_Y.hap1
             Sample_Y.hap2
;
END;
BEGIN CHARACTERS;
       DIMENSIONS NCHAR=20289;
       FORMAT MISSING=? GAP=- MATCHCHAR=. datatype=nucleotide;
MATRIX
Sample_X.hap1
ATCGGACGTTTACGAAAATCG...
sample_X.hap2
ATCGGACGTGAACGAACCTCG...
sample_Y.hap1
ATCGGACGTGTACGAAAATCG...
sample_Y.hap2
ATCGGACGTGTACGAAGATCA...
;
END;
```

After the NEXUS alignments, add the trait information as follows:

```
BEGIN TRAITS;
Dimensions NTRAITS=5;
Format labels=yes missing=? separator=Comma;
TraitLabels AFR EUR EAS SAS AMR;
MATRIX

Sample_X.hap1 1,0,0,0,0
sample_X.hap2 1,0,0,0,0
sample_Y.hap1 0,1,0,0,0
sample_Y.hap2 0,1,0,0,0
;
END;
```

In this example, we are adding five continental ancestries: AFR, EUR, EAS, SAS, and AMR. The total number of ancestries/traits was defined as "Dimensions NTRAITS=5". We also defined the labels after "TraitLabels", separated by space.

For each sample/haplotype, the ancestry was set following the order of "TraitLabels," where "1" is true and 0 is false. In this example, Sample_X is from AFR ancestry, and sample_Y is from EUR ancestry.

Finally, save your modified NEXUS file.

# Step 4: Load alignment file in PopArt

Once having a correctly formatted NEXUS file, network construction should be straight forward with PopArt.

Download and install PopArt following the instructions from their [official website](https://popart.maths.otago.ac.nz/download/). We need to load our modified NEXUS file clicking on the "NEX" button.

![SS5](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS5.png?raw=true)

> If you are unibale to load your file, make sure "Files of type:" option at the bottom of the window is set to "All Files(*)."

After loading your NEXUS file, the information of traits and nucleotide sequences will be displayed on "Traits" and "Alignment" tabs.

![SS6](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS6.png?raw=true)

Now you can construct the network using the algorithm of your choice, clicking on network tab. I chose a Minimum Spanning Network with epsilon=0.

![SS7](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS7.png?raw=true)

To add trait color to the network, click on the dots icon on the menu and choose a color palette.

![SS8](https://github.com/dcsoto/dcsoto.github.io/blob/master/assets/img/2024-09-30-haplotype_network/SS8.png?raw=true)

You can customize trait colors, vertex and edge colors and sizes, as well as labels in the "Edit" tab.

And that's it! Now you can analyze your haplotype network to assess signatures of selection.
