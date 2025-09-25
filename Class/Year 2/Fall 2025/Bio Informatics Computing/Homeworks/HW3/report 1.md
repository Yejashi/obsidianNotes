# COSC594 – Homework 3 Report

**Name:** Befikir Bogale  
**Class:** COSC594  
**Assignment:** Homework 3

---

## 1. Simulate a Hidden Markov Model
I implemented the hidden markov model for the dishonest casino in Python. The executable is `casino_simulator.py`.  

**Usage:**  
```bash
usage: casino_simulator.py [-h] [--show-states] [--seed SEED] [--output OUTPUT] [sequence_length]

Generates a random sequence of dice rolls.

positional arguments:
  sequence_length  Length of the sequence to generate (default: 300)

options:
  -h, --help       show this help message and exit
  --show-states    If set, also show which die (F or L) produced each roll.
  --seed SEED      Optional random seed for reproducible sequences.
  --output OUTPUT  Optional file name to dump the sequence.
```

Example output:
```
./casino_simulator.py          
Printing Sequence of length 300
4 6 1 6 6 3 6 6 6 6 
3 4 6 6 3 6 6 2 6 2 
6 6 6 5 6 5 3 2 3 5 
5 6 6 2 6 3 2 4 1 4 
1 1 5 2 3 4 4 3 4 2 
6 2 3 4 6 2 6 5 4 6 
6 6 6 4 4 1 3 3 6 6 
5 6 6 3 6 5 6 1 6 1 
6 6 5 6 4 4 6 6 4 4 
1 3 6 3 2 6 3 4 1 3 
6 2 6 6 6 6 2 3 5 3 
5 1 2 4 2 2 6 6 2 3 
5 4 5 1 2 4 5 3 6 6 
3 1 5 6 1 5 5 4 3 5 
5 5 4 2 6 6 4 6 6 6 
6 6 5 4 2 1 6 6 6 2 
1 5 5 6 4 6 6 4 4 6 
6 6 6 6 6 2 6 1 2 1 
4 1 5 5 5 2 3 4 3 4 
1 2 4 5 1 5 3 5 5 6 
6 5 1 3 5 2 6 6 2 6 
3 2 6 2 3 4 6 4 1 2 
3 1 3 5 4 5 1 4 6 6 
6 4 5 2 1 3 4 6 6 4 
1 1 6 5 6 6 2 2 6 5 
1 1 5 6 6 6 6 6 5 3 
4 6 1 5 6 6 6 6 6 2 
2 4 3 5 3 5 3 3 6 4 
4 2 1 1 5 3 4 4 4 5 
3 6 3 5 1 6 5 2 1 1 
```
## 3. Forward Algorithm – Compute Probabilities
I implemented the forward algorithm  in Python. The executable is `forward.py`.  

