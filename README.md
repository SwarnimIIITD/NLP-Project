#### NLP-Project
#### Preprocessing step -
#### def preprocess_data(data):
#### preprocessed_data = []
#### for item in data:
#### aspects = []
#### for aspect in item['aspect_terms']:
#### aspects.append(aspect['term'])
#### tokens = word_tokenize(item['sentence'])
#### length = len(tokens)
#### labels = ['O'] * length
#### for aspect in item['aspect_terms']:
#### start_index = int(aspect['from'])
#### end_index = int(aspect['to'])
#### aspect_part = item['sentence'][start_index:end_index+1]
#### aspect_tokens = word_tokenize(aspect_part)
#### aspect_length = len(aspect_tokens)
#### for i in range(length):
#### if tokens[i] == aspect_tokens[0]:
#### labels[i] = 'B'
#### for j in range(aspect_length-1):
#### labels[i+j+1] = 'I'
#### break
#### preprocessed_data.append(
#### {
#### 'sentence' : item['sentence'],
#### 'tokens' : tokens,
#### 'labels' : labels,
#### 'aspect_terms' : aspects,
#### }
#### )
#### return preprocessed_data
#### Have first made a function to do preprocessing. In that function, take all the aspect terms from each data point in the data and take terms from each aspect term. This is appended in a list which contains all aspect terms for a sentence. Similarly, take each data point and extract the start and end index of each aspect term.With help of that, have aspect term part from sentence Tokenize that part of the aspect term from the sentence and try to find there starting within
#### tokenization of that specific sentence. Wherever there is starting assigned B of BIO indexing and I till length of aspect term extracted (O is assigned to all remaining part in begging itself).
#### Finally, append this new labels list of tokenize sentences (each word label), aspect term list for the specific sentence, tokenize sentence and sentence itself is saved in dictionary form to the final list to have all data points of this format/structure.
#### Model Architecture & Hyperparameter used :-
#### Model 1 -
#### Rnn layer followed by two fully connected layers and each fully connected layer is followed by Relu activation function and dropout layer. FInal one fully connected layer to get output
#### Rnn ((batch_size, sequence_length, input_dim) → (batch_size, sequence_length, hidden_dim)) ->
#### fully connected layer (hidden_dim → hidden_dim)->
#### relu ->
#### dropout layer ->
#### fully connected layer (hidden_dim → hidden_dim) ->
#### relu ->
#### dropout layer ->
#### Fully connected layer (hidden_dim → output_dim)
#### Model 2 -
#### GRU layer followed by two fully connected layers and each fully connected layer is followed by Relu activation function and dropout layer. FInal one fully connected layer to get output
#### GRU ((batch_size, sequence_length, input_dim) → (batch_size, sequence_length, hidden_dim)) ->
#### fully connected layer (hidden_dim → hidden_dim) ->
#### relu ->
#### dropout layer ->
#### fully connected layer (hidden_dim → hidden_dim) ->
#### relu ->
#### dropout layer ->
#### Fully connected layer (hidden_dim → output_dim)
#### Hyperparameters -
#### Input dimension, hidden dimension, output dimension, dropout probab, batch_first
#### Training & Validation Loss plot :-
#### Blue line -> Training Loss, Red line -> Validation Loss
#### Plot1 - RNN + Glove
#### Plot2 - GRU + Glove
#### Plot3 - GRU + FastText
#### Plot4 - RNN + FastText
#### Model Comparison :-
#### F1 score ranking ->
#### rnn + glove > gru + glove > gru + fasttext > rnn + fasttext
#### F1 chunk score ranking ->
#### rnn + glove > gru + glove > gru + fasttext > rnn + fasttext
#### F1 Tag score ranking ->
#### rnn + glove > gru + glove > gru + fasttext > rnn + fasttext
#### RNN + Glove f1 0.8147603008421049 f1_chunk 0.6811704213688271 f1_tag 0.9483501803153829
#### GRU + Glove f1 0.8137980366707451 f1_chunk 0.6794268561818558 f1_tag 0.9481692171596341
#### GRU + Fasttext f1 0.7836185498143601 f1_chunk 0.6240937762144577 f1_tag 0.9431433234142622
#### RNN + Fasttext f1 0.780435504410999 f1_chunk 0.6193113284578059 f1_tag 0.941559680364192
#### Best Performance Model -> RNN + Glove f1 0.8147603008421049
#### f1_chunk 0.6811704213688271 f1_tag 0.9483501803153829
