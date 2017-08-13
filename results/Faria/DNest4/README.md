## Faria - DNest4

contributors: João Faria and Brendon Brewer  
online repository: https://github.com/j-faria/EPRVlnZ


### overview

This directory contains my results, obtained with the Diffusive Nested Sampling (DNS) algorithm,
as described in [Brewer+2009](https://arxiv.org/abs/0912.2380) 
and implemented in [DNest4](https://github.com/eggplantbren/DNest4).

The DNS algorithm is an extension of Nested Sampling, which samples from a mixture of successively constrained distributions,
instead of using one single hard constraint at each step.
One advantage over classic Nested Sampling is that this mixture of distributions contains the prior,
which can help when sampling multimodal distributions.
The algorithm provides estimates for the posterior distributions of the parameters, together with the value of the evidence.  
We use a custom implementation of the quasi-periodic kernel and the multivariate Gaussian likelihood, with the correlated noise parameters fixed to the input values.


### details

For all datasets, I used 2 DNS particles and ran the algorithm for 5000 steps. This will mean a different number of posterior samples for each model and each dataset.  
The maximum number of levels is determined automatically.  
The results are computed automatically for all datasets, without any intervention.  
The code ran on a 4-core desktop and the performance metric reported is number of seconds to completion.

### reports


I could only report the evidence estimates, for lack of time to create the other files.  
In any case, all data is available for each run (and actually re-running everything does not imply a very serious computational effort).

I'm not sure if I would trust the **distribution** of evidence estimates as much as their average value. 
Therefore, the quantile range may be underestimated. 

