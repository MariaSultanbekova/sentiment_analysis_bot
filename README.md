# Hi!
Recently, an idea came to me: why not make a bot that will warn me about the emotional coloring of the audio message? 
I often wanted to have this thing😅

To implement this idea, we will need to turn an audio message into text,
then train a neural network that will determine 
whether the message is positive or not(so that we can say that we don't have headphones or come up with another excuse),
and then embed it all into the chat bot


## Model Architecture


Before we go on to explain the architecture of the model that we will use, let's remember what attention is.

The attention mechanism consists of a sequence of encoders and decoders

![head](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/encoder-decoder.png)

Encoders try to put the meaning of a sentence into a small encoded state, and the decoder looks at the hidden state of the encoders and, performing a mathematical operation, receives an attention score. These numbers show how important each encoder state is to the decoder. Then we apply softmax and get the weights, which we multiply by each state of the encoder and then add them up to get one attention output. This attention output vector is additional information about the sentence and allows you to work with input data of huge length

![head](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/attention_score.png)

--------------------------------------------------------------------------------------------------------------
## Now we can move on to the architecture of our model from the transformers library, called BERT. 

A transformer is a sequence of encoders and decoders, but the encoders here are unusual. 

Inside it is the Self-Attention mechanism and a fully connected network. 

![header](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/transformer_encoder.png)


## Self-Attention
A sentence comes to the input of the self-attention block, then each word is encoded into embedding and 3 vectors, called query, key and value:
- the query vector is the encoded information of where one is looking from
- a key vector is information about what is being looked at
- the value vector contains the essence of the word

Then we perform some mathematical operations, which are shown in the picture.

A word that has passed through the Self-Attention mechanism turns into a vector z. We have several Self-Attention heads, each of which conveys a special semantic meaning to the vector (it's like with convolutional neural networks, each core is looking for its patch in the picture) and therefore several z vectors.


