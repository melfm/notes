# R-CNN: Regions with CNN features

## Object detection with R-CNN
- Initial system consisted of three modules :
    - The first generates category-independent region proposals.
    These proposals define the set of candidate detections available
    to the detector.
    - The second module is a large CNN that extracts a fixed-length
    feature vector from each region.
    - Third module is a set of class-specific linear SVMs

### Region proposals
- Selective search to select the proposals

### Feature extraction
- 4096-dimensional feature vector from each region proposal
- Features computed by forward propagating a mean-subtracted
$227 x 277$ RGB image through 5 conv layers and 2 ridge(fc) layer.
- To compute features for a region proposal, need to convert the
image data in that region into a form that is compatible with CNN.
One way is to warp all pixels in a tight bounding box around it to
the required size. Prior to warping, dilate the tight bounding box
so that at the warped size there are exactly $p$ pixels of warped
image around the orignal box.

![RCNN Network](images/RCNN_arch.png)

# Fast R-CNN

## R-CNN and SPPnet
- R-CNN is slow because it performs a ConvNet forward pass for
each object proposal, without sharing computation.
- Spatial pyramid pooling networks (SPPnet) were proposed to
speed up R-CNN by sharing computation.
- SPPnet computes a convolutional feature map for the entire
input image and then classifies each object proposal using a
feature vector extracted from the shared feature map.
- SPPnet has drawbacks:
    - Training is a multi-stage pipeline that involves extracting
    features, fine-tuning a network with log loss, training SVMs
    and finally fitting bounding-box regressors.

## Fast R-CNN Architecture
- Method to fix the disadvantage of R-CNN and SPPnet
- Higher mAP
- Training is single-stage using a multi-task loss
- Training can update all network layers
- No disk storage needed for caching

![Fast RCNN Network](images/Fast_RCNN_arch.png)

### Training
- Takes as input an entire image and a set of object proposals
- The network first process the whole image with several conv and
max pooling layers to produce a conv feature map.
- For each object proposal a region of interest (RoI) pooling layer
extracts a fixed-length feature vector from the feature map.
- Each feature vector is fed into a sequence of fc layers that finally
branch into two siblin output layers:
    - One that produces softmax probability estimates over $K$ object
    classes plus a catch-all ''background'' class and another layer
    that outputs four real-values numbers for each of the $K$ object
    classes.
    - Each set of 4 values encodes refined bounding-box position for
    one of the $K$ classes.

### RoI pooling layer
- uses max pooling to convert the features inside any valid region of
interest into a small feature map with a fixed spatial extent of $H \times W$.
- RoI is a rectangular window into a conv feature
- Each RoI is defined by a four-tuple $(r,c,h,w)$ that specifies its
top-left corner $(r,c)$ and its height and width $(h,w)$.
- RoI max pooling works by dividing the $h \times w$ RoI window into a
$H \times W$ grid of sub-windows of approximate size $h/H  \times w/W$
and then max-pooling the values in each sub-window into the corresponding
output grid cell.
- Pooling is applied independently to each feature map channel.
- The RoI layer is just special-case of the spatial pyramid pooling layer
used in SPPnets in which there is only one pyramid level.


# Faster R-CNN


