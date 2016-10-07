# Tensorflow RNN
Tensorflow provides a number of methods for constructing Recurrent Neural Networks.

## tf.nn.runn
Creates a recurrent neural network specified by RNNCell cell.
Simplest form of network :

state = cell.zero_state(...)

outputs = []

for input\_ in inputs:
  output, state = cell(input\_, state)
  outputs.append(output)
  return (output, state)

- Initial state can be provided
- If the sequence\_length vector is provided, dynamic calculation is performed?
