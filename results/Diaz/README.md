## Díaz - Perrakis estimator

### contributor: Rodrigo Díaz

### Overview


Results with the Perrakis et al. estimator <http://www.sciencedirect.com/science/article/pii/S0167947314000814?via%3Dihub>. This is an importance sampling estimator using the product of the marginal posterior distributions of the parameters as importance sampling function.

### Details

The estimator requires the density of the marginal likelihood of each parameter or block of parameters. To do this, we simply adopt the value of a normalised histogram.

The production of samples from the importance sampling function is done shuffling a sample from the joint posterior obtained previously with an  MCMC algorithm (emcee, in this case).

We run the code taking 5000 samples from the importance sampling function. The Perrakis estimator is biased, so it should be verified that convergence was reached. I usually do this by computing the estimator for different sizes on samples from the importance sampling function, and study the evolution of the result. Although I didn't do this in this case, I checked that doubling the sample size did not change the value of the estimator significantly.

### Computing time
As we repeated the computation 2000 times to estimate the distribution of log10(Z), I've used 5000x2000 for benchmark, as is the number of calls to the likeihood function that are needed