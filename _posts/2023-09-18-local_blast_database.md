---
layout: post
title: How to set up your local BLAST database
subtitle: Bioinformatics diaries #1
show-avatar: false
tags: [bioinformatics]
permalink: /2023/09/18/local_blast_database/
---

I have been working as a bioinformatician for ~8 years, but for some reason I never had to set up my own local Blast database. Until now. 

And I found it to be either really easy if you know what to do but harder to figure out that it should.

Shout-out to this blog for setting me on the right track: https://danielbruzzese.wordpress.com/

So, here it is. A quick little guideline to set up and use Blast in your local cluster.

## Step 0: Load your module

```bash
module load blast/2.12.0+
```

## Step 1: Download the database 

We need to generate a folder where we will download both the Blast database and the taxonomy database.

```bash
mkdir -p my_blastdb
```

Let's get into our new folder:

```bash
cd my_blastdb
```

Here, we are downloading the nucleotide database and asking the software to automatically decompress the files.

```bash
update_blastdb.pl --decompress nt
```

A bunch of files starting with `nt.XX.YY` should be in your database folder.

## Step 2: Download taxonomy

To add taxonomy information, we need to manually download the taxonomy database and decompress.

```bash
update_blastdb.pl taxdb
tar -zxvf taxdb.tar.gz
```

Two additional files should now be in your database folder: `taxdb.bti` and `taxdb.btd`.

## Step 3: Let's blast

We are ready to actually Blast. Let's go to our working directory.

To use our local database, we need to add the path + the prefix of our files. In my example:
```
/PATH/TO/my_blastdb/nt
```

To obtain the species of our subject sequences, we need to manually request the `staxids` (Subject Tax IDs). Blast formats 6, 7, and 10 can be customize to add `staxids`.

```bash
blastn -num_threads 34 -db /PATH/TO/my_blastdb/nt -query input.fa -out output.out -outfmt “7 qseqid qlen slen qcovhsp sseqid staxids bitscore score evalue pident qstart qend sstart send”
```

And that's it. Enjoy Blasting!
