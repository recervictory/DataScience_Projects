# Objectived
1. Learn to create, train and evaluate a recurrent neural network model with TensorFlow and Keras.
2. Learn to train a sequence to sequence recurrent net to be able to solve simple addition equations given in string format.

# Project Structure
The hands on project on Simple Recurrent Neural Network is divided into following tasks:

## Task 1: Introduction
In this project, we want to create a RNN model and train it to learn the meanings of various characters and understand a simple plus operation. The model needs to infer the meaning of various characters and then learn addition from the given data. RNNs are perfect for solving a problem like this because both the input and output are sequences. So, the model must learn the sequence of the input and then predict a sequence for the output.

## Task 2: Generate Data
We know that the model that we’d create will need numeric values in tensors as input. Basically, we know that we can’t simply input the characters as is - we will have to create a suitable representation of the characters and ultimately of the entire sequences, before we can feed the data to a model. We will do this by converting the characters to one-hot-encoded vectors. The dimension of the vector will be equal to the length of our all the characters in our lexicon. These are the total number of features we have.

## Task 3: Create the Model
The model that we are making has two sections to it. The first part, which is the encoder, is a single SimpleRNN layer with a bunch of hidden units. The output of this layer will be a single vector representation of the input. To achieve this single vector representation of the entire input, we will use the RepeatVector layer and specify the number of times it should repeat. Then the vector representation of the input is fed into a decoder part of the model. This is another RNN layer which will take the vector representation of the input and generate a predicted sequence. Each time step in the output sequence needs to predict probabilities for the various possible characters that the each time step can have. So, we will use a Dense layer with the softmax activation function to do this. The only tricky part is that we want to encapsulate the layer inside a TimeDistributed layer so that the model knows that we want to apply the Dense layer to individual time steps and the hidden state is different for different time steps.

## Task 4: Vectorize and De-vectorize the Data
So, we have the model that we’d like to train. We have the data as well but it’s not in the format that we’d want. We want to vectorize the string data so that it can be used with our RNN model. Let’s define a function to vectorize a pair of example and label generated from the generate_data function we wrote before. We will write another function to de-vectorize an example back into string. This is because while we only need the vectorized examples for our model, we will still need to convert some test examples back into human readable format so that we, humans, can read them.

## Task 5: Create Dataset
Let’s define a function to create our dataset. We are defining this function because, later when we need another dataset for testing, we can re-use the code. This is simple to do and we will just use a for loop to create one-hot-encoded representations of the randomly generated data from the previously defined generate_data function.

## Task 6: Training the Model
Before we train the model, we will create a couple of callbacks. A LambdaCallback to simplify our logging. We may end up training the model for a couple of hundred epochs so to simplify the logs during training, we will use a lambda function to print out just the validation accuracy. We also use the EarlyStopping callback. Let’s monitor validation loss and give it a fairly high patience, say 10 epochs. We are also going to use a slightly high batch size to speed up the training and a 20% validation split.
After the training is complete, we will create a test set and take a look at some of the predicted sequences.
