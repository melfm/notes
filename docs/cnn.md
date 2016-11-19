# ConvNets

- Sequence of layers, every layer transforms one volume of activations to another through a differentiable function.
- Using three main types of layers to build ConvNet architectures: Convolutional Layer, Pooling Layer and Fully-connected Layer.
Example architecture :

- INPUT [32x32x3] will hold the raw pixel values of the image
- CONV layer : computes the output of neurons that are connected to local regions in the input, each computing a dot product between their weights and a small region
they are connected to in the input volume. So say we use 12 filters, this results in -> [32x32x12]
-
