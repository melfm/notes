# Neural Networks

# Weight Initialization
One should generally initialize weights with a small amount of noise for symmetry breaking and to prevent 0 gradients.
If using ReLU neurons, it is good practce to initialize them with a slightly positive initial bias to avoid 'dead neurons'.

# Ways to reduce overfitting
- Weight-decay
- Weight-sharing
- Early stopping
- Model averaging
- Bayesian fitting of neural nets
- Dropout

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
