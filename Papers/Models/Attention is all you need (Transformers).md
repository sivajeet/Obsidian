 
- Encoders - Decoders
- English to German translation
- No Recurrent neural network
- seq-seq model 
- Got rid of recurrence and convolutions but only kept attention 

**Recurrent models** generate the sequence of hidden state h(t) a function of the previous hidden state h(t-1) and the input for position t. resulting in criticality in longer sequences, memory problem.

**Attention** helps in up-weighting and down-weighting the dependencies, without focusing on their distance.

Self-attention: Up-weight the sentences more relevant for the task, down-weight the sentences less relevant

Seq2Seq: English seq to German seq

You first feed one word, then another, no parallel computing( but today's GPU?)

Input embedding: Similar words are closer to each other in a vector space

Positional encoder: Vector that gives context based on the position of word in sentence

Liner : another feed-forward layer, to expands the dimention based on output.

Softmax: Probability, human interpreatable

Architecture:

Multi-head attention: Compute the attention of each word based on interactions with other words, multiple attention blocks per word, then averaged vectors to get attention for each word


Q, K, V vectors for every single word

Read Pervasive attention, Bert models