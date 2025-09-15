# EX3 Implementation of GSP Algorithm In Python
### DATE: 15-09-2025
### NAME: Mahalakshmi R
### REG :212223230116
## AIM: 
To implement GSP Algorithm In Python.
## Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
## Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

## Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

## Program:

```python
from collections import defaultdict
from itertools import combinations

def generate_candidates(dataset, k, min_support):
    candidates = defaultdict(int)
    for seq in dataset:
        flat_seq = [item for itemset in seq for item in itemset]
        for comb in combinations(flat_seq, k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

def gsp(dataset, min_support):
    fp = defaultdict(int)
    k = 1
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset = [
    [["a","b","c"], ["b","e"], ["c","f","g"], ["a","b","e"]],   
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],       
    [["b","c"], ["a","d"], ["e","b","f"], ["c","d","f","g","h"]], 
    [["c"], ["e","c"], ["e","h"]]                             
]

dataset2 = [
    [["b","d"], ["c","b"], ["a","c"]],  
    [["b","f"], ["c","e"], ["b"], ["f","g"]],       
    [["a","h"], ["b","f"], ["a","b","f"]],
    [["b","e"], ["c","e"], ["d"]],   
    [["a"], ["b","d"], ["b","c","b"], ["a","d","e"]]
]

min_support = 3

results = gsp(dataset, min_support)

print("Frequent Sequential Patterns for Dataset 1:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
    


results = gsp(dataset2, min_support)

print("\nFrequent Sequential Patterns for Dataset 2:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
```
## Output:
```

Frequent Sequential Patterns for Dataset 1:
Pattern: ('a',), Support: 4
Pattern: ('b',), Support: 6
Pattern: ('c',), Support: 9
Pattern: ('e',), Support: 5
Pattern: ('f',), Support: 4
Pattern: ('g',), Support: 3
Pattern: ('d',), Support: 3
Pattern: ('h',), Support: 3
Pattern: ('a', 'b'), Support: 6
Pattern: ('a', 'c'), Support: 6
Pattern: ('a', 'e'), Support: 4
Pattern: ('a', 'f'), Support: 4
Pattern: ('a', 'g'), Support: 3
Pattern: ('b', 'c'), Support: 9
Pattern: ('b', 'b'), Support: 4
Pattern: ('b', 'e'), Support: 6
Pattern: ('b', 'f'), Support: 7
Pattern: ('b', 'g'), Support: 5
Pattern: ('b', 'a'), Support: 3
Pattern: ('c', 'b'), Support: 4
Pattern: ('c', 'e'), Support: 7
Pattern: ('c', 'c'), Support: 6
Pattern: ('c', 'f'), Support: 7
Pattern: ('c', 'g'), Support: 6
Pattern: ('c', 'a'), Support: 3
Pattern: ('e', 'c'), Support: 3
Pattern: ('e', 'f'), Support: 3
Pattern: ('f', 'g'), Support: 4
Pattern: ('a', 'd'), Support: 3
Pattern: ('d', 'c'), Support: 4
Pattern: ('d', 'f'), Support: 4
Pattern: ('d', 'g'), Support: 3
Pattern: ('d', 'h'), Support: 3
Pattern: ('b', 'h'), Support: 3
Pattern: ('c', 'h'), Support: 7
Pattern: ('f', 'h'), Support: 3
Pattern: ('b', 'd'), Support: 3
Pattern: ('c', 'd'), Support: 3
Pattern: ('e', 'h'), Support: 3
Pattern: ('a', 'b', 'c'), Support: 7
Pattern: ('a', 'b', 'b'), Support: 3
Pattern: ('a', 'b', 'e'), Support: 6
Pattern: ('a', 'b', 'f'), Support: 5
Pattern: ('a', 'b', 'g'), Support: 4
Pattern: ('a', 'c', 'b'), Support: 3
Pattern: ('a', 'c', 'e'), Support: 3
Pattern: ('a', 'c', 'c'), Support: 4
Pattern: ('a', 'c', 'f'), Support: 5
Pattern: ('a', 'c', 'g'), Support: 5
Pattern: ('a', 'e', 'f'), Support: 3
Pattern: ('a', 'f', 'g'), Support: 4
Pattern: ('b', 'c', 'b'), Support: 5
Pattern: ('b', 'c', 'e'), Support: 5
Pattern: ('b', 'c', 'c'), Support: 5
Pattern: ('b', 'c', 'f'), Support: 9
Pattern: ('b', 'c', 'g'), Support: 8
Pattern: ('b', 'c', 'a'), Support: 4
Pattern: ('b', 'b', 'e'), Support: 4
Pattern: ('b', 'b', 'f'), Support: 3
Pattern: ('b', 'e', 'c'), Support: 3
Pattern: ('b', 'e', 'f'), Support: 4
Pattern: ('b', 'e', 'g'), Support: 3
Pattern: ('b', 'e', 'b'), Support: 3
Pattern: ('b', 'f', 'g'), Support: 7
Pattern: ('b', 'a', 'b'), Support: 3
Pattern: ('b', 'a', 'e'), Support: 3
Pattern: ('c', 'b', 'e'), Support: 4
Pattern: ('c', 'b', 'f'), Support: 3
Pattern: ('c', 'e', 'c'), Support: 3
Pattern: ('c', 'e', 'f'), Support: 3
Pattern: ('c', 'c', 'f'), Support: 3
Pattern: ('c', 'c', 'g'), Support: 3
Pattern: ('c', 'f', 'g'), Support: 7
Pattern: ('c', 'a', 'b'), Support: 3
Pattern: ('c', 'a', 'e'), Support: 3
Pattern: ('e', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'c'), Support: 4
Pattern: ('a', 'd', 'f'), Support: 4
Pattern: ('a', 'd', 'g'), Support: 3
Pattern: ('a', 'd', 'h'), Support: 3
Pattern: ('a', 'c', 'h'), Support: 4
Pattern: ('a', 'f', 'h'), Support: 3
Pattern: ('d', 'b', 'c'), Support: 4
Pattern: ('d', 'b', 'f'), Support: 3
Pattern: ('d', 'c', 'c'), Support: 3
Pattern: ('d', 'c', 'f'), Support: 3
Pattern: ('d', 'c', 'g'), Support: 3
Pattern: ('d', 'c', 'h'), Support: 4
Pattern: ('d', 'f', 'g'), Support: 4
Pattern: ('d', 'f', 'h'), Support: 4
Pattern: ('d', 'g', 'h'), Support: 3
Pattern: ('b', 'c', 'h'), Support: 6
Pattern: ('b', 'f', 'c'), Support: 3
Pattern: ('b', 'f', 'h'), Support: 5
Pattern: ('b', 'g', 'h'), Support: 3
Pattern: ('c', 'c', 'h'), Support: 5
Pattern: ('c', 'f', 'c'), Support: 3
Pattern: ('c', 'f', 'h'), Support: 5
Pattern: ('c', 'g', 'h'), Support: 4
Pattern: ('f', 'g', 'h'), Support: 3
Pattern: ('b', 'c', 'd'), Support: 4
Pattern: ('b', 'd', 'f'), Support: 4
Pattern: ('b', 'd', 'g'), Support: 3
Pattern: ('b', 'd', 'h'), Support: 3
Pattern: ('c', 'd', 'f'), Support: 4
Pattern: ('c', 'd', 'g'), Support: 3
Pattern: ('c', 'd', 'h'), Support: 3
Pattern: ('c', 'e', 'h'), Support: 4
Pattern: ('a', 'b', 'c', 'b'), Support: 4
Pattern: ('a', 'b', 'c', 'e'), Support: 4
Pattern: ('a', 'b', 'c', 'c'), Support: 4
Pattern: ('a', 'b', 'c', 'f'), Support: 6
Pattern: ('a', 'b', 'c', 'g'), Support: 6
Pattern: ('a', 'b', 'c', 'a'), Support: 3
Pattern: ('a', 'b', 'b', 'e'), Support: 4
Pattern: ('a', 'b', 'f', 'g'), Support: 5
Pattern: ('a', 'c', 'b', 'e'), Support: 4
Pattern: ('a', 'c', 'f', 'g'), Support: 5
Pattern: ('a', 'e', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'b', 'e'), Support: 5
Pattern: ('b', 'c', 'b', 'f'), Support: 3
Pattern: ('b', 'c', 'e', 'f'), Support: 3
Pattern: ('b', 'c', 'c', 'f'), Support: 3
Pattern: ('b', 'c', 'c', 'g'), Support: 3
Pattern: ('b', 'c', 'f', 'g'), Support: 9
Pattern: ('b', 'c', 'f', 'a'), Support: 3
Pattern: ('b', 'c', 'f', 'b'), Support: 3
Pattern: ('b', 'c', 'f', 'e'), Support: 3
Pattern: ('b', 'c', 'g', 'a'), Support: 3
Pattern: ('b', 'c', 'g', 'b'), Support: 3
Pattern: ('b', 'c', 'g', 'e'), Support: 3
Pattern: ('b', 'c', 'a', 'b'), Support: 4
Pattern: ('b', 'c', 'a', 'e'), Support: 4
Pattern: ('b', 'b', 'f', 'g'), Support: 3
Pattern: ('b', 'e', 'c', 'f'), Support: 3
Pattern: ('b', 'e', 'c', 'g'), Support: 3
Pattern: ('b', 'e', 'f', 'g'), Support: 4
Pattern: ('c', 'b', 'f', 'g'), Support: 3
Pattern: ('c', 'e', 'f', 'g'), Support: 3
Pattern: ('c', 'c', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'b', 'c'), Support: 4
Pattern: ('a', 'd', 'b', 'f'), Support: 3
Pattern: ('a', 'd', 'c', 'c'), Support: 3
Pattern: ('a', 'd', 'c', 'f'), Support: 3
Pattern: ('a', 'd', 'c', 'g'), Support: 3
Pattern: ('a', 'd', 'c', 'h'), Support: 4
Pattern: ('a', 'd', 'f', 'g'), Support: 4
Pattern: ('a', 'd', 'f', 'h'), Support: 4
Pattern: ('a', 'd', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'h'), Support: 4
Pattern: ('a', 'b', 'f', 'h'), Support: 3
Pattern: ('a', 'c', 'c', 'h'), Support: 3
Pattern: ('a', 'c', 'f', 'h'), Support: 3
Pattern: ('a', 'c', 'g', 'h'), Support: 3
Pattern: ('a', 'f', 'g', 'h'), Support: 3
Pattern: ('d', 'b', 'c', 'c'), Support: 3
Pattern: ('d', 'b', 'c', 'f'), Support: 3
Pattern: ('d', 'b', 'c', 'g'), Support: 3
Pattern: ('d', 'b', 'c', 'h'), Support: 4
Pattern: ('d', 'b', 'f', 'g'), Support: 3
Pattern: ('d', 'b', 'f', 'h'), Support: 3
Pattern: ('d', 'c', 'c', 'h'), Support: 3
Pattern: ('d', 'c', 'f', 'g'), Support: 3
Pattern: ('d', 'c', 'f', 'h'), Support: 3
Pattern: ('d', 'c', 'g', 'h'), Support: 3
Pattern: ('d', 'f', 'g', 'h'), Support: 4
Pattern: ('b', 'c', 'c', 'h'), Support: 4
Pattern: ('b', 'c', 'f', 'c'), Support: 3
Pattern: ('b', 'c', 'f', 'h'), Support: 6
Pattern: ('b', 'c', 'g', 'h'), Support: 5
Pattern: ('b', 'f', 'g', 'h'), Support: 5
Pattern: ('b', 'f', 'c', 'h'), Support: 3
Pattern: ('c', 'f', 'g', 'h'), Support: 5
Pattern: ('c', 'f', 'c', 'h'), Support: 3
Pattern: ('b', 'c', 'd', 'f'), Support: 5
Pattern: ('b', 'c', 'd', 'g'), Support: 4
Pattern: ('b', 'c', 'd', 'h'), Support: 4
Pattern: ('b', 'a', 'd', 'f'), Support: 3
Pattern: ('b', 'd', 'f', 'g'), Support: 4
Pattern: ('b', 'd', 'f', 'h'), Support: 4
Pattern: ('b', 'd', 'g', 'h'), Support: 3
Pattern: ('c', 'a', 'd', 'f'), Support: 3
Pattern: ('c', 'd', 'f', 'g'), Support: 4
Pattern: ('c', 'd', 'f', 'h'), Support: 4
Pattern: ('c', 'd', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'b', 'e'), Support: 5
Pattern: ('a', 'b', 'c', 'f', 'g'), Support: 6
Pattern: ('a', 'b', 'c', 'f', 'a'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'a'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'a', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'a', 'e'), Support: 3
Pattern: ('b', 'c', 'b', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'e', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'c', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'a'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'b'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'a', 'b'), Support: 3
Pattern: ('b', 'c', 'f', 'a', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'g', 'a', 'b'), Support: 3
Pattern: ('b', 'c', 'g', 'a', 'e'), Support: 3
Pattern: ('b', 'c', 'g', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'a', 'b', 'e'), Support: 3
Pattern: ('b', 'e', 'c', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'c'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'f'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'g'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'h'), Support: 4
Pattern: ('a', 'd', 'b', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'b', 'f', 'h'), Support: 3
Pattern: ('a', 'd', 'c', 'c', 'h'), Support: 3
Pattern: ('a', 'd', 'c', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'c', 'f', 'h'), Support: 3
Pattern: ('a', 'd', 'c', 'g', 'h'), Support: 3
Pattern: ('a', 'd', 'f', 'g', 'h'), Support: 4
Pattern: ('a', 'b', 'c', 'c', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'f', 'g', 'h'), Support: 3
Pattern: ('a', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('d', 'b', 'c', 'c', 'h'), Support: 3
Pattern: ('d', 'b', 'c', 'f', 'g'), Support: 3
Pattern: ('d', 'b', 'c', 'f', 'h'), Support: 3
Pattern: ('d', 'b', 'c', 'g', 'h'), Support: 3
Pattern: ('d', 'b', 'f', 'g', 'h'), Support: 3
Pattern: ('d', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'h'), Support: 6
Pattern: ('b', 'c', 'f', 'c', 'h'), Support: 3
Pattern: ('b', 'c', 'a', 'd', 'f'), Support: 3
Pattern: ('b', 'c', 'd', 'f', 'g'), Support: 5
Pattern: ('b', 'c', 'd', 'f', 'h'), Support: 5
Pattern: ('b', 'c', 'd', 'g', 'h'), Support: 4
Pattern: ('b', 'a', 'd', 'f', 'g'), Support: 3
Pattern: ('b', 'a', 'd', 'f', 'h'), Support: 3
Pattern: ('b', 'd', 'f', 'g', 'h'), Support: 4
Pattern: ('c', 'a', 'd', 'f', 'g'), Support: 3
Pattern: ('c', 'a', 'd', 'f', 'h'), Support: 3
Pattern: ('c', 'd', 'f', 'g', 'h'), Support: 4
Pattern: ('a', 'b', 'c', 'f', 'g', 'a'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'a', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'a', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'b', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'a', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'a', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'b', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'a', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'a', 'b'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'a', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'a', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'g', 'a', 'b', 'e'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'c', 'h'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'f', 'g'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'f', 'h'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'g', 'h'), Support: 3
Pattern: ('a', 'd', 'b', 'f', 'g', 'h'), Support: 3
Pattern: ('a', 'd', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('d', 'b', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('b', 'c', 'a', 'd', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'a', 'd', 'f', 'h'), Support: 3
Pattern: ('b', 'c', 'd', 'f', 'g', 'h'), Support: 5
Pattern: ('b', 'a', 'd', 'f', 'g', 'h'), Support: 3
Pattern: ('c', 'a', 'd', 'f', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'a', 'b'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'a', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'b', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'a', 'b', 'e'), Support: 3
Pattern: ('a', 'b', 'c', 'g', 'a', 'b', 'e'), Support: 3
Pattern: ('b', 'c', 'f', 'g', 'a', 'b', 'e'), Support: 3
Pattern: ('a', 'd', 'b', 'c', 'f', 'g', 'h'), Support: 3
Pattern: ('b', 'c', 'a', 'd', 'f', 'g', 'h'), Support: 3
Pattern: ('a', 'b', 'c', 'f', 'g', 'a', 'b', 'e'), Support: 3

Frequent Sequential Patterns for Dataset 2:
Pattern: ('b',), Support: 10
Pattern: ('d',), Support: 4
Pattern: ('c',), Support: 5
Pattern: ('a',), Support: 5
Pattern: ('f',), Support: 4
Pattern: ('e',), Support: 4
Pattern: ('b', 'd'), Support: 6
Pattern: ('b', 'c'), Support: 7
Pattern: ('b', 'b'), Support: 6
Pattern: ('b', 'a'), Support: 6
Pattern: ('d', 'c'), Support: 3
Pattern: ('d', 'b'), Support: 3
Pattern: ('c', 'b'), Support: 3
Pattern: ('b', 'f'), Support: 6
Pattern: ('b', 'e'), Support: 6
Pattern: ('c', 'e'), Support: 3
Pattern: ('a', 'b'), Support: 6
Pattern: ('a', 'f'), Support: 3
Pattern: ('a', 'd'), Support: 3
Pattern: ('b', 'd', 'c'), Support: 3
Pattern: ('b', 'd', 'b'), Support: 3
Pattern: ('b', 'c', 'b'), Support: 4
Pattern: ('b', 'c', 'a'), Support: 3
Pattern: ('b', 'b', 'a'), Support: 4
Pattern: ('d', 'b', 'a'), Support: 3
Pattern: ('b', 'f', 'g'), Support: 3
Pattern: ('b', 'c', 'e'), Support: 4
Pattern: ('a', 'b', 'f'), Support: 4
Pattern: ('a', 'b', 'a'), Support: 4
Pattern: ('a', 'b', 'b'), Support: 4
Pattern: ('h', 'b', 'f'), Support: 3
Pattern: ('b', 'c', 'd'), Support: 3
Pattern: ('a', 'b', 'd'), Support: 4
Pattern: ('a', 'b', 'e'), Support: 3
Pattern: ('a', 'd', 'e'), Support: 3
Pattern: ('b', 'd', 'e'), Support: 4
Pattern: ('b', 'b', 'd'), Support: 3
Pattern: ('b', 'b', 'e'), Support: 3
Pattern: ('b', 'a', 'd'), Support: 3
Pattern: ('b', 'a', 'e'), Support: 3
Pattern: ('b', 'd', 'b', 'a'), Support: 3
Pattern: ('b', 'c', 'b', 'a'), Support: 3
Pattern: ('a', 'h', 'b', 'f'), Support: 3
Pattern: ('a', 'b', 'd', 'e'), Support: 4
Pattern: ('a', 'b', 'b', 'a'), Support: 3
Pattern: ('a', 'b', 'b', 'd'), Support: 3
Pattern: ('a', 'b', 'b', 'e'), Support: 3
Pattern: ('a', 'b', 'a', 'd'), Support: 3
Pattern: ('a', 'b', 'a', 'e'), Support: 3
Pattern: ('b', 'b', 'a', 'd'), Support: 3
Pattern: ('b', 'b', 'a', 'e'), Support: 3
Pattern: ('b', 'b', 'd', 'e'), Support: 3
Pattern: ('b', 'a', 'd', 'e'), Support: 3
Pattern: ('a', 'b', 'b', 'a', 'd'), Support: 3
Pattern: ('a', 'b', 'b', 'a', 'e'), Support: 3
Pattern: ('a', 'b', 'b', 'd', 'e'), Support: 3
Pattern: ('a', 'b', 'a', 'd', 'e'), Support: 3
Pattern: ('b', 'b', 'a', 'd', 'e'), Support: 3
Pattern: ('a', 'b', 'b', 'a', 'd', 'e'), Support: 3




```
## Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category, top_k=15):
    if result:
        # Sort patterns by support (descending)
        sorted_items = sorted(result.items(), key=lambda x: x[1], reverse=True)[:top_k]
        patterns = [str(p) for p, _ in sorted_items]
        support = [s for _, s in sorted_items]

        plt.figure(figsize=(10, 6))
        plt.plot(patterns, support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")


results1 = gsp(dataset, min_support)
results2 = gsp(dataset2, min_support)

visualize_patterns_line(results1, "Dataset 1")
visualize_patterns_line(results2, "Dataset 2")
```
## Output:
<img width="929" height="542" alt="image" src="https://github.com/user-attachments/assets/90c19dcd-6b24-4aa8-bcfe-a742b7bc66fc" />

<img width="924" height="545" alt="image" src="https://github.com/user-attachments/assets/3b6ccfb0-f51a-4a55-90e2-f7fc7855cedc" />

## Result:
The GSP algorithm successfully generated frequent sequential patterns for both datasets.
