## 2013 Mikolov W2V Notes  
### Hierarchical Softmax
This is basically the standard whenever the network needs to predict a term when the dictionary is big, say, 250,000 words. If we calculate the activation value of all the nodes and then the softmax probability, the computation cost would be too high. Hence, we encode the tree using a Huffman tree [^footnote]. Afterwards we initiate L many neurons where L is the length of the tree, where the output of each neuron represents the decision of left/right from the root down to the leaf. And the word corresponding to the leaf of the roll-out, is the prediction of the model.

[^footnote]: Recall how to make a Huffman tree: Firstly calculate the frequency of each word. Repeatly at each turn, assign a respective '0' and '1' as the prefix of both the least frequent terms, and combine the two to be one new term. Until there's only one term which appears to be the root of the Huffman tree, the assignment achieves the shortest coding length possible.

### Negative Sampling
Plain training process tries to maximize the probability of predicting the correct term. To make the model more power at distinguishing the correctness and randomness, the model instead maximizes the difference of log probabilities of the ground truth and some random words. To see the details of drawing random words, checkout the paper section.

### Subsample Frequent Words
The colocation of frequent words with other words are meaningless. Hence the model discard each word with probability (1 - f**(-1/2)).

## 2015 T2V Notes
### LDA
It firstly conduct LDA to get the topics.

### T2V Network
Take the skip-gram model in W2V. Each time it tries to predict the surrounding words using the current word, it also takes into consider the topic associated with the current word as a second input. Both inputs are embedded and concatenated with each other before fed into the hidden layer. The embeddings of both topics and words are learned in this way.

## 2016 Topicvec Notes
### 大体上是LDA,但是里面的词都向量化了

## Doc2Vec Notes

The most naive way: just learn W2V and average all words in the paragraph to yield the paragraph vector.  
Instead we make it a little bit subtler. Recall that in c-bow each word in the paragraph is predicted using the context i.e. the k words surrounding it. We treat the paragraph itself to be an additional word which is the context of all the words of that paragraph. Here, the document is represented by its ID and is mapped through an embedding layer.
