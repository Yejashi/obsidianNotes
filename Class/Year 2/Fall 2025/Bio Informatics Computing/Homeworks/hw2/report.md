# COSC594 – Homework 1 Report

**Name:** Befikir Bogale  
**Class:** COSC594  
**Assignment:** Homework 2

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

Example use case:
```
> ./model_probability.py 
Multinomial Log Probability: -452.6623122326925
Markov Log Probability: -451.7966057821609
```

Discussion:
The multinomial and Markov models produce similar log-probabilities, with the Markov model slightly less negative. This is probable because the Markov model captures short-range dependencies well since it has a three Nucleotide context as opposed to the multinomial model which only knows about independent Nucleotides. 

## 7. Markov-Based Random Sequence Generator
I implemented `markov_generator.py`, which uses the model from Task 6 to generate a synthetic DNA sequence of 20,000 bases.

```
usage: markov_generator.py [-h] [training_genome_file] [synthetic_output_file]

Generates a sequence of 20,000 bases on a training sequence.

positional arguments:
  training_genome_file
  synthetic_output_file

options:
  -h, --help            show this help message and exit
```

By default, `markov_generator.py` takes `human_mito.fasta` as input and writes to `markov_simulated.fasta`.

**Synthetic sequence frequencies:**
```
===================================
Nucleotide   |    Frequency
A            |   0.3094
C            |   0.3060
G            |   0.1323
T            |   0.2523
===================================
===================================
Dinucleotide |    Frequency
AA           |   0.09585479273963698
AC           |   0.08735436771838592
AG           |   0.05025251262563128
AT           |   0.0759537976898845
CA           |   0.09540477023851193
CC           |   0.1008050402520126
CG           |   0.02425121256062803
CT           |   0.0855042752137607
GA           |   0.03740187009350467
GC           |   0.04295214760738037
GG           |   0.025451272563628183
GT           |   0.02650132506625331
TA           |   0.08075403770188509
TC           |   0.07490374518725937
TG           |   0.032351617580879045
TT           |   0.06430321516075804
===================================
```

Discussion:
To gauge realism, I compared nucleotide and dinucleotide frequencies of the synthetic sequence against the human mitochondrial genome. The synthetic sequence showed a strong bias (e.g., A = 0.309 vs. 0.254 in the real genome), while real genomes distribute nucleotides more evenly. Dinucleotide frequencies in the synthetic data were somewhat closer to realistic distributions but still showed distortions (e.g., inflated AA/CC, underrepresented CG). This indicates that while the third-order Markov model captures some local dependencies, it does not fully reproduce the balanced base composition of real genomes. I think this might highlight a limitation of training the model on just a third order Markov model. Perhaps, the genome will be more balanced if i used more than three nucleotides as context.