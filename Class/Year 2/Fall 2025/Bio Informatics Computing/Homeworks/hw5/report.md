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
The NEIGHBOR (neighbor‐joining) tree and KITSCH (ultrametric) tree were largely similar because both were built from the same DNADIST matrix. However, NEIGHBOR does not assume a molecular clock and allows unequal root‐to‐tip distances, while KITSCH forces an ultrametric tree with equal total path lengths for all taxa. As a result, KITSCH had equalized leaf heights and slightly different branch lengths and clustering compared to NEIGHBOR.

The only differences 