# Region of Interest Pooling


- Object detection network family are usually divided into two subnetworks by the Region-of-Interest
pooling layer
    - A shared ''fully convolutional'' subnetwork independent of RoIs
    - An RoI-wise subnetwork that does not share computation
- For e.g. VGG used a convolutional subnetwork ending with a spatial pooling layer, followed by
several fully-connected $(fc)$ layers
- So the (last) spatial pooling layer in is turned into the RoI pooling layer


## The RoI pooling layer
- Uses max pooling to convert the features inside any valid region of interest
into a small feature map with a fixed spatial extent of $H \times W$ (e.g. $ 7 \times 7$)(hyper-parameter)
- An RoI is a rectangular window into a conv feature map
- Each RoI is defined by four tuple $(r, c, h, w)$ (in 2D) specifying top-left corners, height and width
- RoI max pooling works by dividing the $h \times w$ RoI window into an $H \times W$ grid of sub-windows
of approximate size $\frac{h}{H} \times \frac{w}{W}$ and then max-pooling the values in each sub-window
into the corresponding output grid cell
- Pooling is applied independently to each feature map channel, same as standard max pooling

## Back-propagation through RoI pooling layers
- BP routes derivatives through the RoI pooling layer
- Assume we have one image per mini-batch
- Let $x_i \in R$ be the $i$-th activation input into the RoI pooling layer and let $y_{rj}$
be the layer's $j$-th output from the $r$-th RoI
- The RoI pooling layer computes $y_{rj} = x_{i*(r,j)}$
    - $i * (r,j) = argmax_{i' \in R(r,j)} x_{i'}$
- $R(r, j)$ is the index set of inputs in the sub-window over which the output unit $y_{rj}$ max pools
- A single $x_i$ may be assigned to several different outputs $y_{rj}$
- The RoI pooling layer's backwards function computes the partial derivative of the loss function with
respect to each input variable $x_i$ by following the argmax switches :

\begin{equation}
    \frac{\partial L}{\partial x_i} = \sum_r \sum_j[i = i^* (r,j)]\frac{\partial L}{\partial y_{rj}}
\end{equation}
- For each mini-batch RoI $r$ and for each pooling output unit $y_{rj}$:
    - The partial derivative $\frac{\partial L}{\partial y_{rj}}$ is accumulated if $i$ is the argmax
    selected for $y_{rj}$ by max pooling


# Region-based Fully Conv Net
- R-FCN uses a different technique. It consists of a shared fully conv architecture FCN
- To incorporate translation variance, construct a set of $\textbf{position-sensitive}$ score maps
    - Using a bank of specialized conv layers as the FCN output
- Each of these score maps encodes the position information w.r.t a relative spatial position (say left of an object)
- On top of this, add a positive-sensitive RoI pooling layer that takes info from these score maps, with no
weight (conv or fc) layers following
- So then the entire architecture is end-to-end
- All learnable layers are convolutional and shared on the entire image and encode spatial info

## Position-sensitive score maps
- To encoder position info into each RoI, we divide each RoI rectangle into $k \times k$ bins by a regular grid
- Again for an RoI rectangle of a size $ w \times h$ a bin is $ \approx \frac{w}{k} \times \frac{h}{k}$
- The last conv layer is constructed to produce $k^2$ score maps for each category
- Inside the $(i,j)$-th bin
    - $(0 \leq i,j, \leq k- 1)$
    - Define a position-sensitive RoI pooling op that pools over only the $(i,j$)-th score map

\begin{equation}
    r_c(i,j | \Theta) = \sum_{(x,y) \in bin(i,j)} z_{i,j,c} (x + x_0, y + y_0 | \Theta)/n
\end{equation}
- $r_c(i, j)$ is the pooled response in the $(i,j)$-th bin for the $c$-th category
- $z_{i,j,c}$ is one scope map out of the $k^2(C+1)$ score map
- $(x_0, y_0)$ denotes the top-left corner of an RoI
- $n$ is the number of pixels in the bin
- $\Theta$ denotes all learnable parameters
- So this equation performs average pooling but max pooling can also be done


## Position-sensitive RoI Pooling
- The $k^2$ position-sensitive scores then vote on the RoI
- Voting is done by averaging the scores, producing a $(C+1)$-dimensional vector for each RoI
    - $r_c(\Theta) = \sum_{i,j} r_c(i,j | \Theta)$
- Then we compute the softmax responses across categories

\begin{equation}
    s_c(\Theta) = \frac{e^{r_c (\Theta)}}{\sum^C_{c'=0} e^{r_c' (\Theta)}}
\end{equation}
- They are used for evaluating the cross-entropy loss during training and for ranking the RoIs during inference
- Now for the bounding box regression, aside from the above $k^2(C+1)$-dim conv layer, append a sibling
4$k^2$-d conv layer for bounding box regression
- The position-sensitive RoI pooling is performed on this bank of 4$k^2$ maps, producing a 4$k^2$-d vector
for bounding box as $t = (t_x, t_y, t_w, t_h)$
- There is no learnable layer after the RoI layer, enabling nearly cost-free region-wise computation
and speeding up both training and inference




