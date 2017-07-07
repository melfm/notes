# Single Stage Detector Using Recurrent Rolling Convolution

### Missing piece of current methods
- Faster R-CNN relies on large receptive field of each overlapping
$3 \times 3$ area of the last conv layer to detect small and large objects
- Since multiple pooling layers are used the resulting resolution of the
last feature map is much smaller than the input image
    - Problematic for detecting small objects
- Alternative proposed in SSD :
    - Exploit the fact that in most of the CNN models for detection
    the internal feature maps in different layers are already of different
    scales due to pooling.
    - Utilize higher res feature maps to detect small objects and low
    res for large

### Single Shot Detector (SSD)
- Feed-forward conv net, produces fixed-size collection of BB and scores
- Mutli-scale feature maps for detection
    - Add conv feature layers to the end of the truncated base network
    - These layers decrease in size progressively and allow detection at multiple
scales
- Key difference between training SSD and training a typical detector that uses
region proposals is that GT info needs to be assigned to specific outputs in
the fixed set of detector output

## RRC Overview
- Recurrent process in which iteration gathers and aggregares relevant features
for detection



