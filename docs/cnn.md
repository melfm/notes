# ConvNets

- Sequence of layers, every layer transforms one volume of activations to another through a differentiable function.
- Using three main types of layers to build ConvNet architectures: Convolutional Layer, Pooling Layer and Fully-connected Layer.

Example architecture :
- INPUT [32x32x3] will hold the raw pixel values of the image
- CONV layer : computes the output of neurons that are connected to local regions in the input, each computing a dot product between their weights and a small region they are connected to in the input volume. So say we use 12 filters, this results in -> [32x32x12]
- RELU : applies an elementwise activation function such as $max(0,x)$ thresholding at zero. This leaves the volume unchanged.
- POOL : performs a downsampling operation along the spatial dimension (width, height) -> [16x16x12]
- FC : computes the class scores, resulting in a volume size [1x1x10], if we have 10 categories. Each neuron in this layer will be connected to all the numbers in the previous volume.


Note : Some layers contain parameters and others don't. In particular, CONV/FC layers perform transformations that are a function of both input volume and also parameters (the weights and the biases of the neurons). RELU/POOL however implement a fixed function.
The parameters in the CONV/FC layers are trained with gradient descent.


## Convolutional Layer
This is the core building block. The layer's parameters consist of a set of learnable filters. Every filter is small spatially but extends through the full depth of the input volume. During forward pass, we slide each filter across the width and height of the input volume and compute dot products between the entries of the filter and the input at any position. As we do this we will produce a 2-dimensional activation map that gives the responses of that filter at every spatial position. So this way the network learns filters that activate when they see some type of visual feature such as an edge of some orientation or a blotch of some color. So in this case we will have an entire set of filters in each CONV layer (12 filters) and each will produce a separate 2-dimensional activation map. We then stack these activation maps along the depth dimension and produce the output volume.

In terms of connectivity, the connections are local in space (that is along width and height) but always full along the entire depth.

Let's take an example : Say we have input volume [32x32x3]. If the receptive field (i.e. filter size) is 5x5, then each neuron in the Conv Layer will have weights to a [5x5x3] region in the input volume, so total 5*5*3 = 75 weights plus bias.
Now say the input volume has [16x16x20]. Using filter 3x3, we now have 3*3*20 = 180 connections to the input volume.

### Spatial Arrangement
Three hyperparameters control the size of the output volume: the depth, stride and zero-padding.
1. The depth : corresponds to the number of filters we would like to use, each learning to look for something different in the input. We will refer to a set of neurons that are looking at the same regions of the input as a depth column (or fibre).
2. Stride with which we slide the filter. When the stride is 1 we move the filters one pixel at a time. When the stride is 2 then the filters jump 2 pixels at a time as we slide them around.
3. Sometimes it is convenient to pad the input volume with zeros around the border. The nice feature of zero padding is that it will allow us to control the spatial size of the output volumes.

So in order to compute the spatial size of the output volume, say W = input volume size, F = the receptive field size, S = stride and P = zero padding on the border. So the formula for calculating how many neurons fit is (W - F + 2P)/S + 1.
So if input is 7x7 and 3x3 filter with stride 1 and pad 0 then we get output 5x5. If stride is 2, then 3x3.

### Parameter Sharing
Controls the number of parameters.