# Hi!

Recently, an idea came to me: why not make a bot that will warn me about the emotional coloring of the audio message? 
I often wanted to have this thing😅
This bot can also be used in telegram groups to warn the admin about the possible beginning of a verbal altercation.

To implement this idea, we will need to turn an audio message into text,
then train a neural network that will determine 
whether the message is positive or not(so that we can say that we don't have headphones or come up with another excuse),
and finally embed it all into the chat bot

--------------------------------------------------------------------------------------------------------------
## Now I will briefly talk about the architecture of the neural network that we will use

This is a model from the transformers library, called BERT

The transformer itself is a sequence of encoders and decoders, but the encoders here are unusual. 
Inside it is the Self-Attention mechanism and a fully connected network. 

![header](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/transformer_encoder.png)


## Self-Attention
The sentence enters the encoder, where each word is marked with a position token, and is also translated into embedding (vector, which is a compressed representation of the word). These two vectors add up and arrive at self-attention. There embedding is encoded into 3 other vectors, using multiplication by special matrices query, key and value:

- the query vector is the encoded information of where one is looking from
- a key vector is information about what is being looked at
- the value vector contains the essence of the word

Then we perform some mathematical operations, which are shown in the picture.

A word that has passed through the Self-Attention mechanism turns into a vector z. We have several Self-Attention heads, each of which conveys a special semantic meaning to the vector (it's like with convolutional neural networks, each core is looking for its patch in the picture) and therefore several z vectors.
We concatenate and flatten these vectors by multiplying them by a special matrix

Next we move on to Layer-Norm. It's like skip connections, made to solve the vanishing gradient problem

![](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/layer_norm.png)

## Differences between the BERT model and a simple transformer

The main task of transformers is the translation from one representation to another (machine translation for example). 
The bottom line is that we want to solve other tasks besides language translation, and for this, let's submit a sentence together with a special CLS token.

This token will contain compressed information about the entire text, and then we can use it to solve the classification problem. 
And also, let's solve the problem of language modeling. To do this, let's skip some words in the sentence and try to predict them. And let's solve another problem, is 2 sentences consecutive or not.
We just want the model to rely on context

![head](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/CLS-token_and_language_modeling.png)

BERT was trained based on huge amounts of data from Wikipedia, and we will need to train it a little for our task. To do this, I found a dataset with thousands of reviews on Amazon, which are marked up into positive and negative


Here is the output of our model:

![](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/result.png)

Training code https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/train.ipynb

Well, for audio processing, we'll take the Silero model
https://www.silero.ai/
(Works well and fast)


And the code for the full launch of the bot is here https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/telegram_bot.ipynb

![](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/result_in_telegram.png)

That's all, you can use)
