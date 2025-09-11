# COSC594 – Homework 1 Report

**Name:** Befikir Bogale  
**Class:** COSC594  
**Assignment:** Homework 2

---

## 2. Global Alignment Implementation
I implemented global alignment in Python. The executable is `globalign.py`.  

**Usage:**  
```bash
usage: globalign.py [-h] [query_fasta] [subject_fasta]

Global alignment of two DNA sequences

positional arguments:
  query_fasta
  subject_fasta

options:
  -h, --help     show this help message and exit
```

By default, `globalign.py` takes `drosophila.fasta` and `human_gene.fasta` for input.

**Alignment Output:**
```
❯ ./globalign.py 
===================================
           GLOBAL ALIGNMENT        
Scoring: match=+2, mismatch=-1, gap=-2
Alignment length: 2848
Alignment score:  -1016
===================================

TTCGCACGGCGTGCGTTTGGCTGAACACAGCAGTCTCTTGGCTAAAGCTTTCATGAGCAGTGCATGTAAT
     |           | ||   | | | |||     |  |   |     |   ||| | | | |    
-----A-----------T-GC---AGA-A-CAG-----T--C---A-----C---AGC-G-G-A-G----

AAAAACTGAGATCCAACTATGTTTACATTGCAACCAACTCCAACTGCTATAGGCACCGTGGTTCCCCCAT
      |  |     |  |    | ||  |       ||    | |   |  |    || | |    | |
------T--G-----A--A----T-CA--G-------CT----C-G--GT--G----GT-G-T----CTT

GGTCAGCGGGAACATTGATAGAGCGCCTGCCGTCTTTAGAAGACATGGCTCACAAGGGTCACAGTGGAGT
 |||| ||||  |       | ||  ||| |  |    |  ||| |  | |||      | | | | || 
TGTCAACGGG--C-------G-GCCACTG-C--C----G--GAC-T--C-CAC------C-C-G-GCAG-

AAATCAGCTGGGTGGCGTTTTTGTTGGAGGAAGGCCTTTGCCAGATTCAACACGGCAAAAAATTGTCGAA
  |  |          |   ||| |  | | | | |  |   ||  || |||  ||        |  |  
--A--A----------G--ATTG-T--A-G-A-G-C--T---AG-CTC-ACA--GC--------G--G--

CTGGCACATTCTGGAGCTCGGCCATGTGATATTTCTCGAATTCTGCAAGTATCAAATGGATGTGTGAGCA
  ||| |   |  | || | |   || || ||||| ||||||||||| || || || ||||||||||| |
--GGC-C---C--G-GC-C-G---TGCGACATTTCCCGAATTCTGCAGGTGTCCAACGGATGTGTGAGTA

AAATTCTCGGGAGGTATTATGAAACAGGAAGCATACGACCACGTGCTATCGGAGGATCCAAGCCACGTGT
||||||| || |||||||| |    | | | | |  |    | | | |||  | ||  |   |||   | 
AAATTCTGGGCAGGTATTACG----A-G-A-C-T--G---GC-T-CCATC--A-GA--C---CCA---G-

GGCCACAGCCGAAGTCGTTAGCAAAATTTCGCAGTACAAACGCGAGTGTCCTAGCATATTTGCTTGGGAA
|| || |  ||  || |   |       |   |||  |||| |||  |    ||  ||   ||    |  
GG-CA-A-TCG--GT-G---G-------T---AGT--AAAC-CGA--G----AG--TA---GC----G--

ATTCGGGATAGATTACTTCAGGAGAACGTTTGTACTAACGATAATATACCAAGTGTGTCCTCAATAAACC
|  |         | |  |   |||| | |||||  | | | || ||    |    | || |     |  
A--C---------T-C--C---AGAA-G-TTGTA--AGC-A-AA-AT----A----G-CC-C-----A--

GTGTATTGAGAAACTTGGCTGCGCAAAAGGAGCAGCAAAGCACGGGATCCGGGAGCTCCAGCACATCCGC
  ||| |    ||       |||     ||||  ||    | |  | |||   | ||   |  | |  | 
--GTA-T----AA-------GCG-----GGAG-TGC----C-C--G-TCC---ATCT-TTG--C-T-TG-

CGGCAACTCAATCAGCGCAAAAGTGTCTGTCAGCATCGGTGGCAACGTGAGCAATGTGGCAAGCGGATCG
 ||  |   ||||  ||    |      |  | ||      |  |  | | |  |||  |   | ||  |
-GG--A---AATC--CG----A------G--A-CA------G--A--TTA-C--TGT--C---C-GA--G

AGAGGCACGTTGAGCTCTTCCACCGATCTTATGCAGACAGCCACTCCTCTTAACTCTTCGGAAAGCGGTG
 | ||   | |   ||  |  ||| |    |  | || |   |     | | |  |  |   |||| || 
-G-GG---G-T---CT-GT--ACC-A----A--C-GATA---A-----CAT-A--C--C---AAGC-GT-

GCGCAACGAACTCCGGGGAGGGTAGTGAACAGGAGGCGATTTACGAGAAGCTTCGGCTGTTAAATACTCA
  |   |  | | |    |    | | |||| ||   | | | ||  || | | |||       ||  | 
--G--TC--A-T-C----A----A-TAAACA-GA---GTTCTTCG-CAA-CCT-GGC-------TA-GC-

GCACGCTGCAGGACCAGGACCACTGGAGCCTGCCAGAGCAGCGCCCTTGGTAGGTCAATCACCCAACCAC
| |    |||  | || |   | ||| | | | |||| | | |  | | |||  |  ||     ||  | 
G-A-AAAGCA--A-CA-G---A-TGG-G-C-G-CAGA-C-G-G--CAT-GTA--T-GAT-----AA--A-

CTAGGAACCCGATCCAGCCACCCCCAGCTGGTGCACGGTAACCATCAGGCACTACAGCAGCATCAACAGC
||   ||   |     |        |     |     ||     |   | |  || |  |        ||
CT---AA---G-----G--------A-----T-----GT-----T---G-A--AC-G--G--------GC

AGAGCTGGCCGCCCCGTCACTATTCCGGATCTTGGTACCCCACCTCTCTTAGCGAAATACCCATCTCATC
|||     |||    |  |  |     |  | |||                | |       || | |  |
AGA-----CCG----G--A--A-----G--C-TGG----------------G-G-------CA-C-C--C

GGCTCCCAATATCGCATCCGTTACGGCGTATGCATCAGGACCTTCACTTGCTCACTCACTGAGTCCACCC
 |  |||    | |     |||   | |||| |  | ||          |       |||   |      
-G--CCC----T-G-----GTT---G-GTAT-C--C-GG----------G------GACT---T------

AACGACATCAAAAGCCTGGCCAGTATCGGTCACCAGAGAAACTGCCCCGTTGCAACGGAGGACATACATT
  ||         |  | |||||    ||    |     ||     ||  |   ||    |     |   
--CG---------G--T-GCCAG----GG----C-----AA-----CC--T---AC----G-----C---

TAAAAAAAGAACTTGATGGTCATCAGTCCGATGAAACGGGCTCCGGTGAAGGTGAAAACTCCAATGGTGG
         ||   ||||| | |  | || | | ||       | | ||| | |         | || ||
---------AA---GATGG-C-T--G-CC-A-GCAA-------CAG-GAA-G-G---------A-GG-GG

CGCTTCAAATATAGGAAACACTGAGGATGATCAAGCTCGGCTCATACTAAAAAGAAAGTTGCAACGCAAT
 |          | |    |  ||  || | ||| ||   | ||| |         |||| |||||  | 
-G----------A-G----A--GA--AT-ACCAA-CT---C-CAT-C---------AGTTCCAACG-GA-

CGAACATCTTTCACGAACGACCAGATAGACAGTCTTGAAAAAGAGTTTGAACGAACACACTATCCAGATG
 ||| |   |||| | | |   ||   | |  ||      || |   ||  ||     ||| | ||| ||
-GAAGA---TTCA-G-ATG---AG---G-C--TC------AA-A---TG--CG-----ACT-T-CAGCTG

TTTTTGCCCGCGAACGTTTGGCTGGAAAGATTGGGTTGCCAGAGGCAAGAATTCAGGTTTGGTTCTCAAA
     |  || |||      |||| |||||          | |    ||||  ||    |  || |   |
---AAG--CG-GAA------GCTGCAAAGA----------A-A---TAGAA--CA----TCCTT-T---A

CCGTCGAGCAAAATGGCGTCGCGAGGAGAAGCTGCGAAACCAGCGAAGAACACCAAATTCCACAGGAGCT
 |  |   |  ||         ||| | ||  |  |     |  |  |  | ||    |      | |  
-C--C---C--AA---------GAGCA-AA--T-TG-----A--G--G--C-CC----T------G-G--

AGTGCAACTTCTTCCTCTACATCGGCAACCGCCTCTTTGACTGACAGCCCTAACAGCCTAAGTGCTTGTT
|  |  |           | |   |  |  |    |||||  |  ||    |||  ||  |    ||  |
A--G--A-----------A-A---G--A--G----TTTGA--G--AG----AAC--CC--A----TT-AT

CCTCGCTGCTGTCCGGATCAGCTGGGGGTCCCTCAGTCAGTACCATTAATGGCTTATCGTCTCCAAGCAC
||  | || |||     |    |    |  || | |  ||    |  ||  |   |    ||   ||  |
CC-AGATG-TGT-----T----T----G--CC-C-G--AG----A--AA--G---A----CT---AG--C

ATTGTCTACTAATGTCAATGCTCCAACGCTTGGCGCTGGGATCGATAGCTCTGAAAGCCCAACACCAATC
|  | |  | ||    ||   |   |             ||||  || | ||| |||  | | |  ||| 
A--G-C--C-AA----AA---T---A-------------GATC--TA-C-CTG-AAG--C-A-A-GAAT-

CCGCACATTCGGCCTAGCTGCACCTCTGACAATGACAATGGTCGTCAAAGTGAAGATTGCAGAAGAGTTT
    |||   ||  ||  ||       |    |     |  |  ||    |  | | | | |||| |   
----ACA---GG--TA--TG-------G----T-----T--T--TC----T--A-A-T-C-GAAG-G---

GTTCTCCATGCCCACTTGGCGTTGGCGGGCATCAAAATACTCATCATATCCAGAGCAATGGTCACGCCCA
|    |||     |  | | |  |  | | |  |||| ||| |  | || ||||| ||  |  |    | 
G----CCA-----A-AT-G-G-AGAAGAG-AAGAAAA-ACTGAGGA-AT-CAGAG-AA--G--A----C-

AGGTCATGCACTTGTTCCTGCCATTTCGCCACGACTCAATTTTAATAGTGGTAGTTTCGGCGCGATGTAC
||| |   ||         | ||      ||| || |        ||||  ||  ||   | |    || 
AGG-C---CA---------G-CA-----ACAC-AC-C--------TAGTCATA--TT---C-C----TA-

TCCAACATGCATCATACGGCGTTATCCATGAGCGATTCATATGGGGCGGTTACGCCGATTCCGAGCTTTA
|    || |||   ||    ||| | |   ||| |  |        |    |    |  |    | | | 
T----CA-GCA--GTA----GTT-T-C---AGC-A--C--------C----A----G--T----G-TCT-

ACCACTCAGCTGTCGGTCCGCTGGCTCCGCCATCGCCAATACCGCAACAGGGCGATCTTACCCCTTCCTC
||||   |         ||  |   |   |||    | | ||| | ||    | | |  |       | |
ACCA---A---------CCAAT---T---CCA----C-A-ACC-C-AC----C-A-C--A-------C-C

GTTATATCCGTGCCACATGACCCTACGACCCCCTCCGATGGCTCCCGCTCACCATCACATCGTGCCGGGT
| | | ||| |  | | |     | | |       | ||  ||   |     | || ||   |     ||
GGT-T-TCC-T--C-C-T-----T-C-A-------C-AT--CT---G----GC-TC-CA---T-----GT

GACGGTGGCAGACCTGCGGGCGTTGGCCTAGGCAGTGGCCAATCTGCGAATTTGGGAGCAAGCTGCAGCG
     |||  |  |  ||  |    | | |  ||   |||  ||  | ||      | | | || |||| 
-----TGG--G--C--CGAAC---AGAC-A--CA---GCC-CTC-AC-AA------A-C-ACCTACAGC-

GATCGGGATACGAAGTGCTATCTGCCTACGCGTTGCCACCGCCCCCTATGGCGTCGAGCTCTGCTGCTGA
|  |    | |    |||   | ||||| ||    ||| |  | || |||||    | | ||||  || |
G--C----T-C----TGC---C-GCCTATGC----CCAGCTTCACC-ATGGCAAATAAC-CTGC--CT-A

TTCAAGCTTCTCAGCCGCGTCCAGTGCCAGCGCTAATGTGACCCCACATCACACCATAGCCCAAGAATCA
| ||| |  | |  ||  ||||    ||||| |  |   |||| | | ||| | | |   ||  |   ||
TGCAA-C--C-C--CC-AGTCC----CCAGC-C--A---GACCTC-C-TCATA-C-T---CC-TG---CA

TGCCCCTCTCCGTGTTCAAGCGCGAGCCACTTTGGAGTTGCTCACAGTTCTGGGTTTTCGTCCGACCCGA
||   ||  ||     | | | | |||| | || | | ||   | |    | ||     |  ||    | 
TG---CT-GCC-----C-A-C-C-AGCC-C-TTCG-G-TG---A-A----T-GG-----G--CG----G-

TTTCACCGGCTGTATCTTCGTATGCACATATGAGCTACAATTACGCGTCGTCCGCTAACACCATGACGCC
    |   | | ||   | | ||  ||       ||||    || |  |  || |   || ||| |    
----A---G-T-TA---T-G-AT--AC-------CTAC----AC-C--C--CC-C---CA-CAT-A----

TTCCTCCGCCAGCGGCACATCAGCACACGTGGCCCCGGGAAAACAACAGTTCTTCGCCTCCTGTTTCTAC
    |  | ||   |   | || ||||  |        |     ||||| ||   |    |     | | 
----T--G-CA---G---A-CA-CACA--T--------G-----AACAG-TC--AG----C-----C-A-

TCACCGTGGGTCTAGGAACAGACTGGCGATTTGAGCAGAGAAGCACTGCGAAAGGACTATTTACATAGTT
  |   |  |    ||  |  ||   |    |   | | |  ||||  |      ||   || |      
--A---T--G----GG--C--AC---C----T---C-G-G--GCAC--C------AC---TT-C------

GAATGTATATCTAAAGGAGGCCATAATAAATCGAATTTACATATCTCTTGAAAAATAATGGAGGTTGTAG
      | | |   ||||   |        ||  |||| |    | |           |   || ||| |
------A-A-C---AGGA---C--------TC--ATTT-C----C-C----------CT---GG-TGT-G

AAAAATACATTTGTATGTATAAATTATATAGTTCCGCCCATTAAATCCAATCTATAGTGTAGAATAATTG
     | ||   |  | |   | ||  | ||||   |||   || |  || |       | | || | | 
-----T-CA---G--T-T-CCAGTT-CA-AGTT---CCC-GGAAGT-GAA-C------CT-G-AT-A-T-

GTGTAAATTAAATGATATAATTTTGACAAATAAAAAAAAAAAAAAAAA
|| | || | | ||    ||  || || | |               ||
GTCTCAA-T-ACTG-GCCAAGATT-AC-AGT---------------AA
```

## 3. Local Alignment Implementation
I implemented local alignment in Python. The executable is `localign.py`.  

**Usage:**  
```bash
usage: localign.py [-h] [query_fasta] [subject_fasta]

Local alignment of two DNA sequences

positional arguments:
  query_fasta
  subject_fasta

options:
  -h, --help     show this help message and exit
```

By default, `localign.py` takes `drosophila.fasta` and `human_gene.fasta` for input.

**Alignment Output:**
```
❯ ./localign.py 
===================================
           Local ALIGNMENT        
Scoring: match=+2, mismatch=-1, gap=-2
Alignment length: 1360
Alignment score:  820
===================================

CACAAGGGTCACAGTGGAGTAAATCAGCTGGGTGGCGTTTTTGTTGGAGGAAGGCCTTTGCCAGATTCAA
|| ||  ||||||| ||||| |||||||| ||||| || |||||    ||  ||||  |||| || || |
CAGAACAGTCACAGCGGAGTGAATCAGCTCGGTGGTGTCTTTGTCAACGGGCGGCCACTGCCGGACTCCA

CACGGCAAAAAATTGTCGAACTGGCACATTCTGGAGCTCGGCCATGTGATATTTCTCGAATTCTGCAAGT
| ||||| || ||||| || || || ||    || || ||||| || || ||||| ||||||||||| ||
CCCGGCAGAAGATTGTAGAGCTAGCTCACAGCGGGGCCCGGCCGTGCGACATTTCCCGAATTCTGCAGGT

ATCAAATGGATGTGTGAGCAAAATTCTCGGGAGGTATTATGAAACAGGAAGCATACGACCACGTGCTATC
 || || ||||||||||| |||||||| || |||||||| || || ||   |||  ||||  | || |||
GTCCAACGGATGTGTGAGTAAAATTCTGGGCAGGTATTACGAGACTGGCTCCATCAGACCCAGGGCAATC

GGAGGATCCAAGCCACGTGTGGCCACAGCCGAAGTCGTTAGCAAAATTTCGCAGTACAAACGCGAGTGTC
|| ||    || ||  | || || ||  | ||||| || ||||||||  | ||||| || || ||||| |
GGTGGTAGTAAACCGAGAGTAGCGACTCCAGAAGTTGTAAGCAAAATAGCCCAGTATAAGCGGGAGTGCC

CTAGCATATTTGCTTGGGAAATTCGGGATAGATTACT-TCAGGAGAACGTTTGTACTAACGATAATATAC
|   ||| |||||||||||||| || || |||||||| ||  |||   || ||||| |||||||| ||||
CGTCCATCTTTGCTTGGGAAATCCGAGACAGATTACTGTC-CGAGGGGGTCTGTACCAACGATAACATAC

CAAGTGTGTCCTCAATAAACCGTGTATTGAGAAACTTGGCT-GCGCAAAAGGAGCAGCAAAGCACGGGAT
|||| ||||| ||||||||| | ||  |  | ||| ||||| ||| ||||| | |||  | |  | | | 
CAAGCGTGTCATCAATAAACAGAGTTCTTCGCAACCTGGCTAGCG-AAAAGCAACAG--ATGGGC-GCAG

CCGGGAGCTCCAGCACATCCGCCGGCAACTCAATCAGCGCAAAAGTGTCTGTCAGCATCGGTGGCAACGT
 ||| |  |  |  | |  |   || |  |  | | | ||   |  | | |  ||| | || ||| ||  
ACGGCA--TGTATGATAAACTAAGG-ATGTTGAAC-GGGC---A--GACCGGAAGC-T-GG-GGC-AC--

GAGCAATGTGGCAAGCGGATCGAGAGGCACGTTGAGCTCTTCCACCG-ATCTTATGC-AGACAGCCACTC
  ||    |||   | | |||  | || || ||   |  | |||  | | | || || |||  ||  | |
CCGC--CCTGG-TTG-GTATC-CG-GGGAC-TT---CGGTGCCAGGGCAACCTACGCAAGATGGCTGC-C

CTCTTAACTCTTCGGAAAGCGGTGGCGCA-ACGAACTCCGGGGAGGGTAGTGAACAGGAGGCGATTTACG
  |  |||     ||  || ||  | | | || ||||||    |  ||    ||| ||||  |||| | |
AGC--AACAGGAAGG--AGGGGGAGAGAATACCAACTCC-ATCA--GT-TCCAAC-GGAGAAGATTCA-G

A-GAAGCTTCGGCTGTTAAAT-A-CT-CAGC--ACGCTGC--AGGACCAGGAC-CACTGGAGCCTGCCAG
| || || ||   ||  |  | | ||  |||  | |||||  || |  || ||   ||  |  |  ||| 
ATGAGGC-TCAAATGCGACTTCAGCTGAAGCGGAAGCTGCAAAGAAATAGAACATCCTTTA--C--CCA-

AGCAGCGCCCTTGGTAGGTCAATCACCCAACCACCT-AG-GAACCCGATCCAGCCACCCCCAGCTGGTGC
|| |||    || | ||| |  |     ||     | || |||||| ||  | |||      | |  |||
AG-AGC-AAATT-G-AGG-CCCTGGAGAAAGAGTTTGAGAGAACCC-AT-TATCCA-GATGTG-T-TTGC

ACGGTAACCATCAGGCA-CTACAGCAGCATCAACAGCAGAGCTGGCCGCCCCGTCACTATTCCGGATCTT
 ||  ||  | |  ||| | | |  || ||| ||   | |||  |    |  ||     || |  |||  
CCGAGAAAGA-CTAGCAGCCAAAATAG-ATCTACCTGA-AGCAAGAATACAGGTATGGTTTTCTAATCGA

GGTACCCCACCTCTCTTAG-CGAAATACCCA--TCTCATCG--G-C-TCCCAATATCGCATCCGTTACGG
 |  ||  |        ||  |||| ||  |    |||  |  | |   |||  | | || ||  || | 
AGGGCCAAATGGAGAAGAGAAGAAAAACTGAGGAATCAGAGAAGACAGGCCAGCAACACA-CC--TA-GT

CGTA-TGC-ATCAGGACCTTCACTTGCTCA-CTCACTGAGTCCACCCAACGACATCAAAAGCCTGGCCAG
| || | | |||| | |  | | ||  ||| | | | | ||| | ||||| |  || | | ||   ||| 
CATATTCCTATCA-G-CAGT-AGTT--TCAGCAC-CAGTGTCTA-CCAACCAATTCCACAACC-CACCA-

TATCGG--T-CACCAGAGAAACT-GC-CC-CGTTGCAACGGA-GGACATA-CATTTA-AAAAAAGAACTT
 | |||  | | ||     | || || ||  ||||   || |  |||| | |  | | ||| |   ||  
CACCGGTTTCCTCCTTCACATCTGGCTCCATGTTGGGCCGAACAGACACAGCCCTCACAAACACCTAC-A

GATGGTCATCAGTCCGATGAAACGGGCTCCGGTGAAGGTGAA-AA-CT-CCAATGGTGGCGCTTCA-AAT
|  | ||  | | || |||   |  ||| |    | ||  || || || || || |   | |  ||    
G-CGCTCTGCCG-CCTATG--CCCAGCTTC-ACCATGGCAAATAACCTGCCTAT-GCAAC-CCCCAGTCC

ATAG-GAAACACTGAGGATGATCAAGC-T-CGGCTCA-TA---CTAAAAAGAAAGTTGC-AACGCA--AT
  ||  | || ||    ||  ||  || | | || ||  |   ||     ||| |  ||  |   |  ||
CCAGCCAGAC-CTCCTCATACTCCTGCATGCTGCCCACCAGCCCTTCGGTGAATG-GGCGGAGTTATGAT

-CGAACA-TCTTTCAC-GA-AC-GAC-CAGATAGACAGTCTTGAAAAAGAGTTTGAACGAACA-CACTAT
 |  |||  |   |||  |  | ||| || ||  ||||||  |  || | |      ||  || |||| |
ACCTACACCCCCCCACATATGCAGACACACATGAACAGTC-AGCCAATG-GGCACCTCGGGCACCACT-T

C--CAGATGTTTTTGCCCGCGAACGTTTGGCTG-GAAAGATTGGGTTGCCAGAGGCAAGAATTCAGGTTT
|  |||   |  || ||| |    || || | |    || |   ||| || || |   |||  | | | |
CAACAGGACTCATTTCCC-C--TGGTGTGTCAGTTCCAGTTCAAGTTCCCGGAAG--TGAA-CCTGATAT

GGTTCTCAAACCGTCGAGCAAAATGGC-GT
 | ||||||  | | |  ||| ||  | ||
-G-TCTCAATAC-T-GGCCAAGATTACAGT
```

**Discussion:**
The first immediate thing is that the score is much better in local alignment (820) when compared to global alignment (-1016).  From what i can see, this is because a lot of penalties are incurred when forcing a full length alignment as opposed to a local one which implies that there might be a good evidence of local homology. In terms of length, again the local alignment fares better. 
## 4 and 7. End-Gap Free Alignment
I implemented End-Gap free alignment in Python. The executable is `egfalign.py`.  

**Usage:**  
```bash
usage: egfalign.py [-h] [query_fasta] [subject_fasta]

End-Gap free alignment of two DNA sequences

positional arguments:
  query_fasta
  subject_fasta

options:
  -h, --help     show this help message and exit
```

By default, `localign.py` takes `human_mito.fasta` and `neander_mito.fasta` for input.

## 5. BLAST Comparison

Length of Alignment:  1269
Identity Percentage: 73.43%
E-value: 4e-65















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