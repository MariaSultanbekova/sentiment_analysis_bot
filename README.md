## Hi!
Recently, an idea came to me: why not make a bot that will warn me about the emotional coloring of the audio message? 
I often wanted to have this thing😅

To implement this idea, we will need to turn an audio message into text,
then train a neural network that will determine 
whether the message is positive or not(so that we can say that we don't have headphones or come up with another excuse),
and then embed it all into the chat bot

To begin with, I will tell you about the architecture of the neural network model that we will use, because it is really interesting

The model is called BERT, it's from the transformers library. It consists of a sequence of encoders and decoders

![head](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/encoder-decoder.png)

Encoders try to put the meaning of a sentence into a small encoded state, and the decoder looks at the hidden state of the encoders and, performing a mathematical operation, receives an attention score. These numbers show how important each encoder state is to the decoder. Then we apply softmax and get the weights, which we multiply by each state of the encoder and then add them up to get one attention output. This attention output vector is additional information about the sentence and allows you to work with input data of huge length

![head](https://github.com/MariaSultanbekova/sentiment_analysis_bot/blob/main/attention_score.png)

