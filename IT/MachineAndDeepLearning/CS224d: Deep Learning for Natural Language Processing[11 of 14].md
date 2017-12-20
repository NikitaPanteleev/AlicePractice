[http://cs224d.stanford.edu/syllabus.html](http://cs224d.stanford.edu/syllabus.html)
#Intro to NLP and Deep Learning
Morphological analysis => syntactic =>semantic => discourse
Why NLP is hard?
- world knowledge
- Jane hit June and then she [fell/ran]
- Ambiguity: "I made her duck"

Machine learning field:
- describe your data with features that computer can understand.
- use learning algorithm

*Representation learning* attempts to automatically learn good features
or representations
*Deep learning* algorithms attempt to learn (multiple levels of)
representation and an output
From raw inputs x (e.g. words)

Two ways to solve deep learning problems: neural networks and
graphical probabalistic models. Neural is faster to learn and better
in NLP.

Resons of exploring Deep Learning now?
- DL techniques benefit more from a lot of data
- Faster machines and multicore CPU/GPU help DL
- New models, algorithms, ideas
=>improved perfomance

DL works with many layers. DL + NLP works with vector representation.
Semantics.
Traditional: lambda calculus
DL: vectors + neural networks

Видео было позитивное в плане один graduate student beaten 1 million
dollar answer-question system using Deep Learning. Будем надеяться,
что какой-нибудь другой студент не придумал ту же самую идею.


#Week 2: Word Vectors.
Meaning of the word. WordNet with is-a relations + synonyms.
one-hot representation - for every word is a vector and no
similarity. We should use *cooccurence* matrix X:
 - word appears in entire document (Latent Semantic Analysis)
 - word with window length.
X = n words * n words in each cell the number of occurences two words in
 one windos.

The matrix is sparse and large. We should use 25-1000 vector
representation.
X = U * S * V - U are vector representations
Hacks to improve
 - Cap maximum number of occurences
 - Ramped windows that count closer words more
 - Pearson correlations, set negative to 0. (cov(X,Y)/ sigma(X) * sigma(Y))
## Idea: Learn low-dimensional vectors directly
 - Learning by back-propagation
 - A neural probabilistic language model
 - NLP from scratch
 - word2vec
## Word2vec
Optimize J  = sum over all words & sum over window of log p (wj + i|
wj)

p(wj + i| wj) = exp(v' * v) / sum of exp
d/ dwj

Count based vs direct prediction.

# WEEK 3: Advanced word vector representations: language models, softmax, single layer networks
SGD

Skip-model: compute a true pair (random word and the word in window)
and some set of random pairs.

Intrinsic and extrinsic options.
city-in-state
Chicago - Illinois :: Houston - Texas
More data, more time helps training.

One more evalutaion: human labels: cat -tiger = 0.98 WordSim353

Usage
 - classification of the words.

The SoftMax classifier. d-vectors are classified in c classes.
W = c * d matrix

# Week 4: Neural Networks and backpropagation -- for named entity
  recognition

{xi,yi}N i=1	

# Week 5: Neural networks and backprop.
train/dev/test splits


# Week 9: Recursive networks.
reucursive structure is a grammar tree over sentence.
tree is good for referencing subphrases.
max-margin framework
s(x, y). x - sentence, y is a grammatical tree.

# Week 10: Recursuve networks.
 - paraphrase detection
 
