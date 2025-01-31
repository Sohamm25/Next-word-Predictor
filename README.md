tokenizer used, tokenizer.fit_on_texts([doc_name]) so now index given to each word and last index will be equal to lenght of doc_name 
next is 
input_sequences = []
for sentence in faqs.split('\n'):
  tokenized_sentence = tokenizer.texts_to_sequences([sentence])[0]

  for i in range(1,len(tokenized_sentence)):
    input_sequences.append(tokenized_sentence[:i+1])
we use doc_name .split("\n") and then we store sentences in another variable 
texts_to_sequences() replaces words with their corresponding token IDs.
It requires fit_on_texts() first, so the tokenizer knows the vocabulary. 
Also a tip tokenizer.texts_to_sequences(["Deep learning is amazing", "I love AI"])
output - [[1, 2, 5, 6], []]  # "AI" is ignored because it wasn’t in fit_on_texts()
next we get the sentence of maximum length and add padding of 0. 
Then X and Y are created 
next by using from tensorflow.keras.utils import to_categorical
y = to_categorical(y,num_classes=283) 
we perform one hot encoding 
and then create the model 
model = Sequential()
model.add(Embedding(283, 100, input_length=56))
model.add(LSTM(150))
model.add(LSTM(150))
model.add(Dense(283, activation='softmax')) 
The Sequential model is a good choice because your text prediction task involves a linear flow of data through a relatively straightforward stack of layers.
