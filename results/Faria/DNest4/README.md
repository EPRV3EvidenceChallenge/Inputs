## Faria - DNest4

contributors: João Faria and Brendon Brewer  
online repository: https://github.com/j-faria/EPRVlnZ


### overview

This directory contains results
obtained with the Diffusive Nested Sampling (DNS) algorithm,
as described in [Brewer et al. 2009](https://arxiv.org/abs/0912.2380) 
and implemented in [DNest4](https://github.com/eggplantbren/DNest4).

The DNS algorithm is an extension of Nested Sampling, 
which samples from a mixture of successively constrained distributions,
instead of using one single hard constraint at each step.
One advantage over classic Nested Sampling 
is that this mixture of distributions contains the prior,
which can help when sampling multimodal distributions.
The algorithm provides estimates for the posterior distributions for the parameters,
together with the value of the evidence.  
We use a custom C++ implementation of both the quasi-periodic kernel 
and the multivariate Gaussian likelihood, 
fixing the correlated noise parameters to the input values.


### details

For all datasets, I used 2 DNS particles and ran the algorithm for 100000 steps. This will mean a different number of posterior samples 
for each model and each dataset.  
The maximum number of levels is determined automatically.  
"Convergence" is checked by analysing the posterior weights
as a function of each level's prior mass X, as is standard in DNS.
There is no "global search" step 
(at least not explicitly separated from a "sampling" step),
as the algorithm is always free to explore the full prior volume.
Results are computed automatically for all datasets, 
without dataset-dependent inputs.  
The code ran on a 4-core desktop and the performance metric reported is number of seconds to completion.

For the analysis with constrained priors,
the prior pdf was set to 0 (actually log_prior_pdf=-1E300)
outside of the provided period bounds.
Inside the bounds, the prior is still a Jeffreys between 1.25 and 1E4.
Nothing else was changed from the unconstrained analysis.


The error is calculated from one single run,
by probabilistic re-assignment of X-values to the samples,
as in standard nested sampling.
These errors are very likely over-optimistic. 


### reports


I only report the evidence estimates,
but all the posterior samples were kept and (with moderate effort)
I can provide the parameter estimates.




