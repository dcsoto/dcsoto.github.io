---
layout: post
title: How to set up your local BLAST nucleotide database
subtitle: Bioinformatics diaries No. 1
show-avatar: false
tags: [bioinformatics]
permalink: /2023/09/18/local_blast_database/
---

I have been working as a bioinformatician for ~8 years, but for some reason I never had to set up my own local nucleotide Blast database. Until now. 

And I found it to be a bit complicated if you don't know what to do. So, here it is. A quick little guideline to set up and use Blast in your local cluster.

Shout-out to [this](https://danielbruzzese.wordpress.com/) blog for setting me on the right track.

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
cd /PATH/TO/my_blastdb
```

Here, we are downloading the nucleotide database and asking the software to automatically decompress the files.

```bash
update_blastdb.pl --decompress nt
```

A bunch of files starting with `nt.XX.YY` should be in your database folder.

## Step 2: Download taxonomy

To add taxonomy information, we need to manually download the taxonomy database and decompress.

```bash
cd /PATH/TO/my_blastdb
update_blastdb.pl taxdb
tar -zxvf taxdb.tar.gz
```

Two additional files should now be in your database folder: `taxdb.bti` and `taxdb.btd`.

## Step 3: Let's Blast

We are ready to actually Blast. Let's go to our working directory.

To use our local database, we need to add the path + the prefix of our files. In my example:
```
/PATH/TO/my_blastdb/nt
```

To use our taxonomy database, we need to export the path as follows:
```bash
export BLASTDB="/PATH/TO/my_blastdb" 
```

Also, to obtain the species of our subject sequences, we need to manually request the `staxids` (Subject Tax IDs). Blast formats 6, 7, and 10 can be customize to add `staxids`.

Addressing these two points, we have the following command:

```bash
blastn -num_threads 34 -db /PATH/TO/my_blastdb/nt -query input.fa -out output.out -outfmt "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore staxids sscinames scomnames"
```

(Here, I am requesting default parameters + subject's taxonomy id, scientific name, and common name.)

<details>
  <summary>Default column names for format 6</summary>

<table>
    <tr>
        <td>1</td>
        <td> qseqid  </td>
        <td> query or source (gene) sequence id</td>
    </tr>
    <tr>
        <td>2</td>
        <td> sseqid  </td>
        <td> subject or target (reference genome) sequence id</td>
    </tr>
    <tr>
        <td>3</td>
        <td> pident  </td>
        <td> percentage of identical positions</td>
    </tr>
    <tr>
        <td>4</td>
        <td> length  </td>
        <td> alignment length (sequence overlap)</td>
    </tr>
    <tr>
        <td>5</td>
        <td> mismatch</td>
        <td> number of mismatches</td>
    </tr>
    <tr>
        <td>6</td>
        <td> gapopen </td>
        <td> number of gap openings</td>
    </tr>
    <tr>
        <td>7</td>
        <td> qstart  </td>
        <td> start of alignment in query</td>
    </tr>
    <tr>
        <td>8</td>
        <td> qend    </td>
        <td> end of alignment in query</td>
    </tr>
    <tr>
        <td>9</td>
        <td> sstart  </td>
        <td> start of alignment in subject</td>
    </tr>
    <tr>
        <td>10</td>
        <td>send     </td>
        <td>end of alignment in subject</td>
    </tr>
    <tr>
        <td>11</td>
        <td>evalue   </td>
        <td>expect value</td>
    </tr>
    <tr>
        <td>12</td>
        <td>bitscore </td>
        <td>bit score</td>
    </tr>
</table>

</details>

<details>
  <summary>Additional columns for custom format</summary>

<table>
    <tr>
        <td>qseqid    </td>
        <td>Query Seq-id</td>
    </tr>
    <tr>
        <td>qgi       </td>
        <td>Query GI</td>
    </tr>
    <tr>
        <td>qacc      </td>
        <td>Query accesion</td>
    </tr>
    <tr>
        <td>qaccver   </td>
        <td>Query accesion.version</td>
    </tr>
    <tr>
        <td>qlen      </td>
        <td>Query sequence length</td>
    </tr>
    <tr>
        <td>sseqid    </td>
        <td>Subject Seq-id</td>
    </tr>
    <tr>
        <td>sallseqid </td>
        <td>All subject Seq-id(s), separated by a &#39;;&#39;</td>
    </tr>
    <tr>
        <td>sgi       </td>
        <td>Subject GI</td>
    </tr>
    <tr>
        <td>sallgi    </td>
        <td>All subject GIs</td>
    </tr>
    <tr>
        <td>sacc      </td>
        <td>Subject accession</td>
    </tr>
    <tr>
        <td>saccver   </td>
        <td>Subject accession.version</td>
    </tr>
    <tr>
        <td>sallacc   </td>
        <td>All subject accessions</td>
    </tr>
    <tr>
        <td>slen      </td>
        <td>Subject sequence length</td>
    </tr>
    <tr>
        <td>qstart    </td>
        <td>Start of alignment in query</td>
    </tr>
    <tr>
        <td>qend      </td>
        <td>End of alignment in query</td>
    </tr>
    <tr>
        <td>sstart    </td>
        <td>Start of alignment in subject</td>
    </tr>
    <tr>
        <td>send      </td>
        <td>End of alignment in subject</td>
    </tr>
    <tr>
        <td>qseq      </td>
        <td>Aligned part of query sequence</td>
    </tr>
    <tr>
        <td>sseq      </td>
        <td>Aligned part of subject sequence</td>
    </tr>
    <tr>
        <td>evalue    </td>
        <td>Expect value</td>
    </tr>
    <tr>
        <td>bitscore  </td>
        <td>Bit score</td>
    </tr>
    <tr>
        <td>score     </td>
        <td>Raw score</td>
    </tr>
    <tr>
        <td>length    </td>
        <td>Alignment length</td>
    </tr>
    <tr>
        <td>pident    </td>
        <td>Percentage of identical matches</td>
    </tr>
    <tr>
        <td>nident    </td>
        <td>Number of identical matches</td>
    </tr>
    <tr>
        <td>mismatch  </td>
        <td>Number of mismatches</td>
    </tr>
    <tr>
        <td>positive  </td>
        <td>Number of positive-scoring matches</td>
    </tr>
    <tr>
        <td>gapopen   </td>
        <td>Number of gap openings</td>
    </tr>
    <tr>
        <td>gaps      </td>
        <td>Total number of gaps</td>
    </tr>
    <tr>
        <td>ppos      </td>
        <td>Percentage of positive-scoring matches</td>
    </tr>
    <tr>
        <td>frames    </td>
        <td>Query and subject frames separated by a &#39;/&#39;</td>
    </tr>
    <tr>
        <td>qframe    </td>
        <td>Query frame</td>
    </tr>
    <tr>
        <td>sframe    </td>
        <td>Subject frame</td>
    </tr>
    <tr>
        <td>btop      </td>
        <td>Blast traceback operations (BTOP)</td>
    </tr>
    <tr>
        <td>staxids   </td>
        <td>Subject Taxonomy ID(s), separated by a &#39;;&#39;</td>
    </tr>
    <tr>
        <td>sscinames </td>
        <td>Subject Scientific Name(s), separated by a &#39;;&#39;</td>
    </tr>
    <tr>
        <td>scomnames</td>
        <td>Subject Common Name(s), separated by a &#39;;&#39;</td>
    </tr>
    <tr>
        <td>sblastnames</td>
        <td>Subject Blast Name(s), separated by a &#39;;&#39;   (in alphabetical order)</td>
    </tr>
    <tr>
        <td>sskingdoms</td>
        <td>  Subject Super Kingdom(s), separated by a &#39;;&#39;     (in alphabetical order)</td>
    </tr>
    <tr>
        <td>stitle   </td>
        <td>  Subject Title</td>
    </tr>
    <tr>
        <td>salltitles</td>
        <td>  All Subject Title(s), separated by a &#39;&lt;&gt;&#39;</td>
    </tr>
    <tr>
        <td>sstrand   </td>
        <td>Subject Strand</td>
    </tr>
    <tr>
        <td>qcovs     </td>
        <td>Query Coverage Per Subject</td>
    </tr>
    <tr>
        <td>qcovhsp   </td>
        <td>Query Coverage Per HSP</td>
    </tr>
</table>

</details>

Original [source](https://www.metagenomics.wiki/tools/blast/blastn-output-format-6).

And that's it. Enjoy Blasting!
