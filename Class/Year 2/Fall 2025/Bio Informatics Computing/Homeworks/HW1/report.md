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
```
===================================
Nucleotide   |    Frequency
A            |   0.2542987918023999
C            |   0.23425838109768668
G            |   0.2643189971547565
T            |   0.24712382994515691
===================================
===================================
Dinucleotide |    Frequency
AA           |   0.07612214181150904
AC           |   0.053050452567988286
AG           |   0.056328735489989894
AT           |   0.06880270509886394
CA           |   0.06630791117708913
CC           |   0.05148347456753469
CG           |   0.06418424362384281
CT           |   0.05228758169934641
GA           |   0.06713263644048577
GC           |   0.07453454567947053
GG           |   0.06556565844003216
GT           |   0.057070988227046864
TA           |   0.04474134553926723
TC           |   0.05519473825281953
TG           |   0.07822519123317045
TT           |   0.06896765015154327
===================================
```

## 5.  Additional Sequences
I have successfully downloaded both NC_012920 (`human_mito.fasta`) and AF25446 (`neander_sample.fasta`).

## 6. Sequence Probability Modeling
I implemented `model_probability.py` which trains a multinomial model and a third order Markov model on the Human genome, and outputs the log-probability of both models for the Neandrethal sequence.

```
usage: model_probability.py [-h] [training_genome_file] [test_genome_file]

Sequence probability modeling of genome sequences

positional arguments:
  training_genome_file
  test_genome_file

options:
  -h, --help            show this help message and exit
```

By default, `model_probability.py` takes human_mito.fasta for training_genome_file and `neander_sample.fasta` for test_genome_file.

