# Tensorflow 
### Printing stuff
import tensorflow as tf
sess = tf.InteractiveSession()
# Some tensor we want to print the value of
a = tf.constant([1.0, 3.0])
# Add print operation
a = tf.Print(a, [a], message="This is a: ")
# Add more elements of the graph using a
b = tf.add(a, a).eval()





# RNN APIs
Tensorflow provides a number of methods for constructing Recurrent Neural Networks.

## tf.nn.rnn
Creates a recurrent neural network specified by RNNCell cell.
Simplest form of network :

state = cell.zero_state(...)

outputs = [ ]

for input_ in inputs:

  output, state = cell(input_, state)
  
  outputs.append(output)
  
  return (output, state)

- Initial state can be provided
- If the sequence\_length vector is provided, dynamic calculation is performed?
- It does not compute the RNN steps past the max sequence length of minibatch
- Propagates the state at a sample's sequence length to the final state output

## tf.nn.dynamic_rnn
Identical to rnn, but performs fully dynamic unrolling of inputs.
Internally, rf.nn.rnn creates an unrolled graph for a fixed RNN length.
For instance if you call tf.nn.rnn with inputs having 200 time steps, you create a static graph with 200 RNN steps.
Graph creation is slow, and not able to pass long sequences.
tf.nn.dynamic_rnn solves this by using a tf.while loop to dynamically construct the graph when it is executed.
This means graph creation is faster and you can feed batches of variable size.

## tf.nn.bidirectional_rnn

## tf.nn.bidirectional_dynamic_rnn

## tf.nn.raw_rnn
More primitive version of dynamic_rnn, provides more direct access to the inputs each iteration. More control over when to start and finish reading the sequence, and what to emit for the output.
Example usage: dynamic decoder of a seq2seq model.


## tf.contrib.learn.TensorFlowRNNClassifier
A wrapper for Tensorflow RNN. It accepts rnn_size, cell_type which could be rnn, gru and lstm.



## Ref: Tensorflow API
- https://www.tensorflow.org/versions/r0.11/api_docs/python/nn.html#recurrent-neural-networks
- https://www.tensorflow.org/versions/r0.11/api_docs/python/contrib.learn.html#TensorFlowRNNClassifier
- http://www.wildml.com/2016/08/rnns-in-tensorflow-a-practical-guide-and-undocumented-features/

