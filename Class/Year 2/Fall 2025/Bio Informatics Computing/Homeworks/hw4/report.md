# COSC594 – Homework 4 Report

**Name:** Befikir T. Bogale  
**Class:** COSC594  
**Assignment:** Homework 4

---

## Part A
For this part, I compared the  Ames ancestor sequence with the Ames sequence. I used nucmer to align them and show-snps to list the variants. The results are in the files `ames_comp.delta` and `ames_comp.snps`.

The results showed about 32 total differences, including single-nucleotide changes and small insertions or deletions. Most of these were small and spread across the genome, but a few spots showed large jumps in cordinates, which might suggest small structural diferences. Since both genomes are almost identical overall, these changes make up a very small fraction of the genome and are probably minor variations between the two strains.



## Part B
I compared the test genome to the reference genome using nucmer and show-coords. I looked at   statistics like number of contigs, total length, and N50 size.

| Metric              | Val         |
| ------------------- | ----------- |
| Reference genome    | NC_000913.3 |
| Assembly size       | ≈ 4.99 Mb   |
| Number of contigs   | ≈ 110       |
| N50 (contig length) | ≈ 190 kb    |
| Average contig size | ≈ 45 kb     |
| Alignment identity  | 98–100%     |
| Reference coverage  | ≈ 99%       |
 Based on the alignment, the test genome matched the reference genome very well. The identity was high, and only small gaps or repeats seemed to be missing. There were about 110 contigs, which means the assembly is somewhat fragmented, but it’s still pretty good overall. The N50 value (around 190 kb) means many contigs are fairly long. 