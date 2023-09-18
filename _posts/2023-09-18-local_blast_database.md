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

## Step 3: Let's Blast

We are ready to actually Blast. Let's go to our working directory.

To use our local database, we need to add the path + the prefix of our files. In my example:
```
/PATH/TO/my_blastdb/nt
```

Also, to obtain the species of our subject sequences, we need to manually request the `staxids` (Subject Tax IDs). Blast formats 6, 7, and 10 can be customize to add `staxids`.

Addressing these two points, we have the following command:

```bash
blastn -num_threads 34 -db /PATH/TO/my_blastdb/nt -query input.fa -out output.out -outfmt "6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore staxids sscinames scomnames”
```

(Here, I am requesting default parameters + subject's taxonomy id, scientific name, and common name.)

<details>
  <summary>Default columns names for format 6</summary>

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

<p>
| #  | colnames | description                                       |
| -- | ---------| ------------------------------------------------- |
| 1  | qseqid   |  query or source (gene) sequence id               |
| 2  | sseqid   |  subject or target (reference genome) sequence id |
| 3  | pident   |  percentage of identical positions                |
| 4  | length   |  alignment length (sequence overlap)              |
| 5  | mismatch |  number of mismatches                             |
| 6  | gapopen  |  number of gap openings                           |
| 7  | qstart   |  start of alignment in query                      |
| 8  | qend     |  end of alignment in query                        |
| 9  | sstart   |  start of alignment in subject                    |
| 10 | send     | end of alignment in subject                       |
| 11 | evalue   | expect value                                      |
| 12 | bitscore | bit score                                         |
</p>

</details>

<details>
  <summary>Additional columns for custom format</summary>

<p>
| colnames   | description                                                                |
| ---------- | -------------------------------------------------------------------------- |
| qseqid     | Query Seq-id                                                               |
| qgi        | Query GI                                                                   |
| qacc       | Query accesion                                                             |
| qaccver    | Query accesion.version                                                     |
| qlen       | Query sequence length                                                      |
| sseqid     | Subject Seq-id                                                             |
| sallseqid  | All subject Seq-id(s), separated by a ';'                                  |
| sgi        | Subject GI                                                                 |
| sallgi     | All subject GIs                                                            |
| sacc       | Subject accession                                                          |
| saccver    | Subject accession.version                                                  |
| sallacc    | All subject accessions                                                     |
| slen       | Subject sequence length                                                    |
| qstart     | Start of alignment in query                                                |
| qend       | End of alignment in query                                                  |
| sstart     | Start of alignment in subject                                              |
| send       | End of alignment in subject                                                |
| qseq       | Aligned part of query sequence                                             |
| sseq       | Aligned part of subject sequence                                           |
| evalue     | Expect value                                                               |
| bitscore   | Bit score                                                                  |
| score      | Raw score                                                                  |
| length     | Alignment length                                                           |
| pident     | Percentage of identical matches                                            |
| nident     | Number of identical matches                                                |
| mismatch   | Number of mismatches                                                       |
| positive   | Number of positive-scoring matches                                         |
| gapopen    | Number of gap openings                                                     |
| gaps       | Total number of gaps                                                       |
| ppos       | Percentage of positive-scoring matches                                     |
| frames     | Query and subject frames separated by a '/'                                |
| qframe     | Query frame                                                                |
| sframe     | Subject frame                                                              |
| btop       | Blast traceback operations (BTOP)                                          |
| staxids    | Subject Taxonomy ID(s), separated by a ';'                                 |
| sscinames  | Subject Scientific Name(s), separated by a ';'                             |
| scomnames  | Subject Common Name(s), separated by a ';'                                 |
| sblastname | s Subject Blast Name(s), separated by a ';'   (in alphabetical order)      |
| sskingdoms |   Subject Super Kingdom(s), separated by a ';'     (in alphabetical order) |
| stitle     |   Subject Title                                                            |
| salltitles |   All Subject Title(s), separated by a '<>'                                |
| sstrand    | Subject Strand                                                             |
| qcovs      | Query Coverage Per Subject                                                 |
| qcovhsp    | Query Coverage Per HSP                                                     |
</p>

</details>

And that's it. Enjoy Blasting!
