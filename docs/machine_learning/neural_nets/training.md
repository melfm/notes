# Neural Networks

## Weight Initialization
One should generally initialize weights with a small amount of noise for symmetry breaking and to prevent 0 gradients.
If using ReLU neurons, it is good practce to initialize them with a slightly positive initial bias to avoid 'dead neurons'.

## Overfitting
- Training data contains info about the regularities in the mapping from input to output. But it also contains
sampling error. That is accidental regularities just because of the particular training cases that were chosen.
- When we fit the model, it cannot tell which regularities are real and which are caused by sampling error.

### Prevention
- Get more data!
- Use a model that has the *right* capacity
  - Enough to fit the true regulatiries
  - Not enough to also fit sputious regularities
 - Average many different models
   - Use models with different forms
   - Train the model on different subsets of the training data ("bagging")
 - Bayesian: Use a single neural network architecture but average the predictions made by many different
 weight vectors.

### Ways to limit the capacity
- Architecture : Limit the number of hidden layers and number of units per layer
- Early stopping: Start with small weights and stop the learning before it overfits
- Weight-decay: Give it a number of hidden layers or units per layer that is a little too large, then penalize large weights using penalties or constraints on their squared values (L2 penalty) or absolute values (L1 penalty).
- Noise: Add noise to the weights or the activities.

## Choosing meta parameters
- Wrong method is using lots of alternatives, easy to do but it gives a false impression of how well the method works
- The setting that works best on test set are unlikely to work as well on a new test set drawn from the same distribution.
- Extreme example is where the test set is so random that does not depend on the input.
  - The best architecture will do better than chance on the test set but not expected to do so on a new test set.

### Cross-validation : Better way
- Divide dataset into:
  - Training data: used for learning the parameters
  - Validation data: not used for learning just for deciding what settings work best
  - Testing data: used to get the final data, unbiased estimate
- Divide the dataset into one final test set and $N$ other subsets and train on all but one of those subsets to get
$N$ different estimates of the validation error rate 
  - Called N-fold cross-validation
  - The $N$ estimates are NOT independent.
  
## Early stopping
- When we have a big model and no time to train a model many times or varying weight penalties. 
- Instead start with small weights and as the model trains watch the performance on the validation set.
- As it starts to get worse, stop training.
- The performance on the validation set may fluctuate particularly if the measuring error rate rather than a 
squared error or cross entropy. So hard to decide but keep going until sure and go back to where things were best.

### Why small weights lower the capacity?
- When the weights are very small, every hidden unit is in its linear range
  - A net wirh a large layer of hidden units is linear
  - It has no more capacity than a linear net in which inputs are mapped to the output
- As the weights grow, the hidden units start using their non-linear ranges so the capacity grows.

So in early stopping, we stop when it has the right number of parameters. That is, its optimized the trade off between fitting the true regularities in the data and fitting the spurious regularities.

## Regularization
Different regularization methods have different effects on the learning process. For example L2 regularization penalizes *high weight values*. L1 regularization penalizes weight values that do not equal to *zero*. Adding noise to the weights during learning ensures that the learned hidden representations take *extreme values*. Sampling the hidden representations regularizes the network by pushing the hidden representation to be *binary* during the forward pass which limits the modeling *capacity* of the network.

Standard L2 weight penalty involves adding an extra term to the cost function that penalizes the squared weights. This keeps the weights small unless they have big error derivatives
  
 So looking at the penalty term below, we get this parabolic cost.

![What the penalty term looks like](images/L2weightdecay.png)

![Equations](images/L2weightEq.png)

Sometimes it works better to penalize the absolute values of the weights, like the V shape below.
Plus to use a weight penalty that has negligible effect on large weights, because L1 allows a few large weights.
![Equations](images/L1weightpenalty.png)

## Weight constraints
- Instead of penalizing the squared value of each weight separately, put a constraint on the maximum squared length of the incoming weight vector of each unit.
- Advantages over weight penalties:
  - Easier to select the sensible value because logistic units have a natural scale (so we know what a weight of 1 means)
  - They prevent hidden unit getting stuck near zero with all their weights being tiny and not doing anything useful.
  - Prevent weights exploding

N.B. The penalties are just the La Grange multiplier required to keep the constraints satisfied. 

## MacKay's quick and dirty method of setting weight costs
- Based on the idea that we can interpret weight penalties as doing map estimation so that the magnitude of the weight penalty is related to the tightness of the prior distribution over the weights.
- Mackay showed we can empirically fit both the weight penalties and the assumed noise in the output of the neural net to fit weight penalties without the need for a validation set.

### Estimating the variance of the output noise
- After we have learned a model that minimizes the squared error, we can find the best value for the output noise.
- The best value is the one that maximizes the probability of producing exactly the correct answers after adding Gaussian noise to the output produced by the neural net.
- The best value if found by simply using the variance of the residual errors.

### Estimating the variance of the Gaussian prior on the weights
- After learning a model with some initial choice of variance for the weight prior, do a dirty trick called "empricial Bayes".
	- Set the variance of the Gaussian prior to be whatever makes the weights that the model learned most likely.
		- This violates a lot of presupposition of the Bayesian approach.
		- We are using the data to decide what our prior beliefs are!
	- This is done by simply fitting a zero-mean Gaussian to the one-dimensional distribution of the learned weight values.
		- We could easily learn different variances for different sets of weights.

### MacKay's method :
Choose the ratio of the noise variance to the weight prior variance
- Start with guesses for both the noise variance and the weight prior variance.
- While not bored, lets do some gradient descent learning
	- Do learning using the ratio of the variances as the weight penalty coefficient.
	- Reset the noise variance to be the variance of the residual errors.
	- Reset the weight prior variance to be the variance of the distribution of the actual learned weights.
- Go back to the start of this loop.


## Why it helps to combine models
With a single model we need to choose some capacity for it. If we choose too little capacity, it would be able to fit the regularities in the training data. If we choose too much capacity, it won't be able to fit the sampling error in the particular training set. By using many models, we can get a better tradeoff between fitting the true regularities, and overfitting the sampling error in the data.


### Combining networks: The bias-variance trade-off
- When the amount of training data is limited, we get overfitting.
	- Averaging the predictions of many different models is a good way to reduce overfitting.
	- It helps most when the models make very different predictions.
- For regression, the squared error can be decomposed into a "bias" term and a "variance" term.
	- The bias term is big if the model has too little capacity to fit the data.
	- The variance term is big if the model has so much capacity that it is good at fitting the sampling error in each particular training set.
- So by averaging we can get rid of the variancee (we end up with low bias each individual model has).

Two ways to average models :
- MIXTURE : Combine models by averaging their output probabilities
- PRODUCT : Combine by taking the geometric means of their output probabilities :


![Model averaging](images/product_models.png)


## Dropout: An efficient way to average many large neural nets
- Each time we present a training example, we randomly omit each hidden unit with probability 0.5.
- Randomly sampling from $2^H$ different architectures.

![Model averaging](images/drop_out.png)


## Mixtures of Experts
- Train a number of neural nets, each of which specializes in a different part of the data.
- Assume we have a data set which comes from a number of different regimes.
- Train a system in which one neural net will specialize in each regime and a managing net will look at the input data, and decide which specialist to give it to.
- Not efficient use of data as it is fractionated over these experts, naturally can't be expected to do well with small data sets.

Q. When learning a mixture of experts, it is desirable that each expert specializes in a different area of the input space. But then at test time, how will we know which expert to use?

A. We also learn a "manager" model that sees the input and assigns probabilities for picking each expert.
We then get predictions from all the experts and take their weighted average using the probabilities.
A Mixture of Experts can be seen as an input-dependent model averaging. The input is used to decide how much weight should be assigned to each model and then a weighted average is taken.



  

