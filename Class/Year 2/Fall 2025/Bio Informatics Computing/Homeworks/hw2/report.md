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
The first immediate thing is that the score is much better in local alignment (820) when compared to global alignment (-1016).  From what i can see, this is because a lot of penalties are incurred when forcing a full length alignment as opposed to a local one which implies that there might be a good evidence of local homology. In terms of length, again the local alignment fares better. In terms of biological meaning, i imagine the better alignment of local alignment means that these two species are tangientially related, perhaps through a distant ancestor, instead of being closely related.
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

Note: I am giving the same program for tasks 4 and 7 since my initial implementation used linear space since i only keep track of single columns of both sequences at a time.

**Output:**
```
===================================
     END-GAP-FREE ALIGNMENT        
Scoring: match=+2, mismatch=-1, gap=-2
Alignment score: 620
===================================
```

## 5. BLAST Comparison

Length of Alignment:  1269
Identity Percentage: 73.43%
E-value: 4e-65

**Discussion:**
Compared to my local alignment implementation which had a length of alignment of 1360, the BLAST utility had a length of alignment of 1269 which is somewhat smaller. I think this might be because the BLAST utility uses some heuristics that compute the value differently. On the other hand, since the e value is very small it shows that it is unlikely that this sequence could happen by change. Moreover, the 73.43% identity percentage shows that the two sequences are related.



## 6. BLAST of Mystery Sequence

**Blastn**:
1.
```
Accession: XM_049606281.1
Species: Anopheles coluzzii
Function: sodium channel protein para 
```
2.
```
Accession: XM_061651125.1
Species:  Anopheles gambiae  coluzzii
Function: sodium channel protein para 
```
3.
```
Accession: XM_049606278.1
Species: Anopheles coluzzii
Function: sodium channel protein para 
```

**Blastx**
1.
```
Accession: XP_049294820.1
Species: Anopheles funestus
Function: sodium channel protein para isoform X10 
```

2.
```
Accession: XP_038108858.1
Species: Anopheles funestus
Function: sodium channel protein para isoform X10 
```
1.
```
Accession: XP_049294820.1
Species: Anopheles funestus
Function: sodium channel protein para isoform X10 
```