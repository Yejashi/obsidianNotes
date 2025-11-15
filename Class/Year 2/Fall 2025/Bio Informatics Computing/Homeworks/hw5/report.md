# COSC594 – Homework 5 Report

**Name:** Befikir T. Bogale  
**Class:** COSC594  
**Assignment:** Homework 5

---

## Question 2: Hamming Distance Program
I modified my global alignment code to do hamming distance. The executable is `hamming_distance.py`.  

Example use case:
```
python3 hamming_distance.py  small.fasta      
0       1       15      16      14
1       0       14      15      13
15      14      0       1       1
16      15      1       0       2
14      13      1       2       0
```

## Question 3
![[Bio_251114_215423_page-0001(1).jpg]]

## Question 4
The only differences I see are that NEIGHBOR lets branch lengths vary, while KITSCH forces everything to line up. So KITSCH ends up with same leaf heights and slightly different branch lengths.


## Question 5

**Are the resulting trees similar to those from KITSCH and NEIGHBOR?**

The trees for MUSCLE and clustal look to be mostly similar to KITSCH and NEIGHBOR. One thing i noticed is that EU980375, EU980379, and EU980377 group together. EU980370 and EU980372 also form a somewhat tight cluster. 

**Are the two MSA-based trees similar to each other?**
The MUSCLE tree and the Clustal tree are basically the same tree. Any differences are tiny where mostly branch lengths rounded slightly differently, so for practical purposes they’re identical.

**Briefly describe any major differences or potential biological explanations**
The differences I do see are mostly small rearrangements inside the big cluster of very similar sequences and some changes in branch lengths, especially around things like EU980369, EU980381, EU980365, and EU980366. That’s pretty much what you’d expect, since Clustal/MUSCLE and PHYLIP are using different alignment heuristics and slightly different distance models, so a few columns line up differently and that nudges the inferred distances. On top of that, these are all closely related cytochrome b sequences, so there isn’t a ton of signal — a handful of substitutions or how gaps are treated can easily flip the local branching order without changing the main biological picture (same outgroup, same core clades).