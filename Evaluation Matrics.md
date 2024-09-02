### Precision

Precision = TP/TP+FP

In LLM, P = Matching n-gram/Total no. of n-gram in Candidate

Example 

Reference: "Transformers make everything quick and efficient"  
Candidate: "Transformers Transformers Transformers Transformers"

P = 1

Bad Matrics for such cases.

### BLEU Score

Brevity Penalty = min(1, len(predicted)/len(reference))

BLEU score = BP * $exp(∑i=1N​(wi​∗ln(pi​))$​

- wi​ is the weight for n-gram precision of order i (typically weights are equal for all i)
- pipi​ is the n-gram modified precision score of order i.
- N is the maximum n-gram order to consider (usually up to 4)
