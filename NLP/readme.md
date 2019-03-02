(incomplete version)
# Advancements Overview (from the latest)

- GPT-2: A large-scale unsupervised language model, without task-specific training BY OpenAI (2019 Feb) - *Language Models are Unsupervised Multitask Learners*
- PyText BY Facebook (2018 Dec) - *NLP modeling framework built on PyTorch*
- Bert BY Google (2018 Oct) - *Pre-training of Deep Bidirectional Transformers for Language Understanding*
- Transformers + Unsupervised pre-training By OpenAI (2018 Jun)- *Improving Language Understanding by Generative Pre-Training*
- ElMo, Contextualized Embeddings BY AllenNLP (2018 Mar) - *Deep contextualized word representations*
- CoVe, Contextualized Word Vectors BY Salesforce (2017 Aug) - *Learned in Translation: Contextualized Word Vectors*
- Transformer by Google (2017 Dec) - *Attention Is All You Need*
- Word2Vec by Google (start from 2013) - *Distributed representations of words and phrases and their compositionality*

# Advancements Details

## Bert BY Google (2018 Oct)
* richly bi-directional
* with random mask out (~15%)
* And then make prediction for that masked word

## Transformers + Unsupervised pre-training By OpenAI (2018 Jun)
* use the pre-train transformer’s decoder to build a classifier

## Context-Aware/Contextualized Embeddings (2017-2018)
* ELMo Embeddings (2018) - Embeddings from Language Models
    1. use **bidirectional** language model (biLM) to learn both word (e.g., syntax and semantics) and linguistic context (i.e., to model polysemy)
    2. produce **multiple word embeddings per single word** for different scenarios

## Transformer BY Google (2017 Dec)
### *Attention Is All You Need*
1. Using Self-Attention in encoding
2. And using Attention in decoding

## Google Word Embedding (Word2Vec) (start from 2013)
1. skip-gram





## FastText

- supervised learning
- linear model
- Hierarchical Softmax
  - Huffman Coding
- have n-gram (so it has the order information)

## Doc2Vec

## GloVe

- find the co-occurance of the whole corpus

## CBOW & Skip-gram

- CBOW Continuous Bag-of Words): windowed-words, predict a word
- Skip-gram: a word, to predict the windowed-words

## Word2Vec







Keywords
====
- Language Modeling: a task of predicting the next word in a sequence of words
- OOV (Out of Vocabulary)
