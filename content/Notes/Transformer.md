---
tags:
  - NLP
  - Study
  - DeepLearing
---

[reference video](https://www.youtube.com/watch?v=bCz4OMemCcA)
## Recurrent Neural Networks (RNN)

### Problems
- Slow computation for long sequences
- Vanishing/exploding gradients
- Diminishing contribution of information from long time-step ago.

## Transformer[[@Vaswani2017]]

### Encoder
#### Input embedding
- Sentence -> words(tokens)
- tokens -> input IDs (a numerical representation of the word, don't change through training)
- input IDs -> Embedding (512 dimension vector, $d_{model}=512$, the value changes through training to better represent the meaning of the word in the sentence)

#### Positional encoding
- We want each word to carry some information about its position in the sentence.
	- We want the model to treat words that appear close to each other as "close" and words that are distant as "distant".
- We want the positional encoding to represent a pattern that can be learned by the model.
- Embedding -> Embedding + Positional Encoding
$$
PE(pos,2i)=\sin{\frac{pos}{10000^{2i/d_{model}}}}
$$
$$
PE(pos,2i+1)=\sin(\frac{pos}{10000^{2i/d_{model}}})
$$
- This is calculated once, and the values are reused for both training and inference.
- The sin-cos positional encoding is chosen to allow the model to easily learn to attend by relative positions.

#### Self-attention
- Allows model to relate words to each other
$$
Attention(Q,K,V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

- For the self-attention, all $Q$, $K$, $V$ are the tokenized input sequence matricies of shape $(seq=\text{sequence length}, d_{model}=d_k)$
- The softmax part returns a square matrix$(seq, seq)$, containing the intensity of the relationship between a word and other words in the sentence. *(It looks similar to [[Covariance matrix]])*
- Matrix multiplication of the softmax output with $V$ returns a matrix with the same size as the input matrix. $(seq=\text{sequence length}, d_{model}=d_k)$ containing information about the relationship between a word and all the other words in the sequence, including the positional information, if done positional encoding.
- Self-attention characteristics
	- Self-attention is permutation invariant.
	- Self-attention by itself, has zero learnable parameter.
	- We can control the calculation by sending values in the position that we don't want an interact to $-\infty$, which will make softmax return zero for that word interaction.

#### Multi-head attention
