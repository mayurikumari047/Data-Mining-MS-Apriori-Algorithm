# Data-Mining-MS-Apriori-Algorithm
Mining Algorithm for finding frequent itemsets when there is multiple MIS values for all items.

MS-Apriori is based on level-wise search. It generates all frequent itemsets by making multiple passes over the data.

The key operation in this algorithm as compared to Apriori algorithm is the sorting of the items in I in ascending order of their MIS values. This order is fixed and used in all subsequent operations of the algorithm. The items in each itemset follow this order.

Let Fk denote the set of frequent k-itemsets. Each itemset w is of the following form, {w[1], w[2], …, w[k]}, which consists of items, w[1], w[2], …, w[k], where MIS(w[1]) <= MIS(w[2]) <= … <= MIS(w[k]). 

## Steps in MS-Apriori algorithm: 

1. Performs the sorting on I according to the MIS value of each item (stored in MS).

2. Makes the first pass over the data using the function init-pass(), which takes two arguments the data set T and the sorted items M, to produce the seeds L for generating candidate itemsets of length 2, i.e., C2. init-pass() has two steps:

a) It first scans the data once to record the support count of each item.

b) It then follows the sorted order to find the first item i in M that meets MIS(i).

3. i is inserted into L. 

For each subsequent item j in M after i, 

if j.count/n  MIS(i), then j is also inserted into L, where j.count is the support count of j, and n is the total number of transactions in T.

Frequent 1-itemsets (F1) are obtained from L. 

For each subsequent pass (or data scan), say pass k, the algorithm performs three operations.

a) The frequent itemsets in Fk-1 found in the (k–1)th pass are used to generate the candidates Ck using the MScandidate-gen() function.
However, there is a special case, i.e., when k = 2 (line 6), for which the candidate generation function is different, i.e., level2-candidate-gen().

b) It then scans the data and updates various support counts of the candidates in Ck (line 9–16). For each candidate c, we need to update its support count (lines 11–12) and also the support count of c without the first item, i.e., c – {c[1]}, which is used in rule generation. 

c) The frequent itemsets (Fk) for the pass are identified by {c  Ck | c.count/n  MIS(c[1])}

Candidate generation functions level2-candidate-gen() and MScandidate-gen() are mentioned below.

### Level2-candidate-gen function: 
It takes an argument L, and returns a superset of the set of all frequent 2-itemsets. 

we use |sup(h) - sup(l)| ≤ phi because sup(l) may not be lower than sup(h), although MIS(l) ≤ MIS(h).

We must use L rather than F1 because F1 does not contain those items that may satisfy the MIS of an earlier item (in the sorted order) but not the MIS of itself.

### MScandidate-gen function: 

It is similar to the candidate-gen function in the Apriori algorithm. It also has two steps, the join step and the pruning step. The join step is the same as that in the candidate-gen() function. The pruning step is, however, different.
For each (k-1)-subset s of c, if s is not in Fk-1, c can be deleted from Ck.
However, there is an exception, which is when s does not include c[1] (there is only one such s). That is, the first item of c, which has the lowest MIS value, is not in s. Even if s is not in Fk-1, we cannot delete c because we cannot be sure that s does not satisfy MIS(c[1]), although we know that it does not satisfy MIS(c[2]), unless MIS(c[2]) = MIS(c[1]).

## Reference: Web_Data_Mining__2nd_Edition__Exploring_Hyperlinks__Contents__and_Usage_Data
