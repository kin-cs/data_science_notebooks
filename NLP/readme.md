(incomplete version)
# Advancements Overview (from the latest)

- OpenAI (2019, Feb) a large-scale unsupervised language model, without task-specific training - *Language Models are Unsupervised Multitask Learners*
- Facebook (2018, Dec) PyText - *NLP modeling framework built on PyTorch*
- Google (2018, Oct) Bert - *Pre-training of Deep Bidirectional Transformers for Language Understanding*
- OpenAI (2018, June): transformers + unsupervised pre-training - *Improving Language Understanding by Generative Pre-Training*


# Advancements Details

## BERT
* richly bi-directional
* with random mask out (~15%)
* And then make prediction for that masked word

## OpenAI Transformer + Unsupervised pre-training 
* use the pre-train transformer’s decoder to build a classifier

## Context-Aware/Contextualized Embeddings
* ELMo Embeddings - Embeddings from Language Models
    1. use **bidirectional** language model (biLM) to learn both word (e.g., syntax and semantics) and linguistic context (i.e., to model polysemy)
    2. produce **multiple word embeddings per single word** for different scenarios

## Word Embedding (Word2Vec)
1. One trick: Skip-gram





## FastText

- supervised learning
- linear model
- Hierarchical Softmax
  - Huffman Coding
- have n-gram (so it has the order information)


## CBOW & Skip-gram

- CBOW: windowed-words, predict a word
- Skip-gram: a word, to predict the windowed-words

## Word2Vec


## GloVe

- find the co-occurance of the whole corpus

Doc2Vec
-------



Keywords
====
- OOV (Out of Vocabulary)
