# COSC594 – Homework 1 Report

**Name:** Befikir Bogale  
**Class:** COSC594  
**Assignment:** Homework 1  

---

## 1. Academic Integrity Statement  
I have read and agree to the terms of the COSC 494/594 Honor Code.  

---

## 2. Retrieve a Genome Sequence  
Downloaded NC_001416.1 and saved it as `lambda.fasta`.  

---

## 3. Reverse Complement Generator  
I implemented the reverse complement generator in Python. The executable is `reverse_complement.py`.  

**Usage:**  
```bash
usage: reverse_complement.py [-h] [input_file_path] [output_file_path]

Reverse-complement a genome

positional arguments:
  input_file_path
  output_file_path

options:
  -h, --help        show this help message and exit
```
    

By default, `reverse_complement.py` takes `lambda.fasta` for input and writes to `lambda.rev.fasta`.

## 4. Nucleotide and Dinucleotide Frequencies

I calculated the nucleotide and dinucleotide frequencies in python. The executable is frequency_analysis.py

```
usage: frequency_analysis.py [-h] [input_file_path]

Frequency analysis of nucleotides and dinucleotides of a genome

positional arguments:
  input_file_path

options:
  -h, --help       show this help message and exit
```

By default, frequency_analysis.py takes lambda.fasta for input_file_path

Summary table for `lambda.fasta`: