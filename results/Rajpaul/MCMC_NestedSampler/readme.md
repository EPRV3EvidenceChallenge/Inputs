# Vinesh Maguire-Rajpaul

## Algorithm overview

+ The results I have submitted for the first data set were obtained from a nested sampling implementation written in MATLAB, based heavily on code written by Pitkin & Romano, available [here](https://github.com/mattpitkin/matlabmultinest). 
+ The code uses the MCMC sampler from [Veitch & Veccio](https://arxiv.org/abs/0911.3820) to generate samples within a standard nested sampling routine. 
+ Note: this is not the same sampler as MultiNest by [Feroz, Hobson and Bridges](http://xxx.lanl.gov/abs/0809.3437) (see comments below).

## General comments

+ While the parameter posterior estimates seem to me to be plausible, I suspect the absolute estimates of evidences may be off by a few orders of magnitude. In a relative sense however the estimates might still OK. E.g., (log evidence for 3 planets - log evidence for 2 planets) could be of the correct order even if there was a problem with overall normalisation. Or...even the odds ratios could be way off...I dunno!
+ Re: the problematic log evidences, I suspect something is going wrong with sampling from the priors, though I have not had time to diagnose the problem. Hopefully I'll be able to fix this for the other data sets. 
+ In addition to the algorithm sketched above, I would have liked to have applied MultiNest (my usual go-to), though I am currently having some minor issues getting (Py)MultiNest working on my laptop. Time permitting, I do still hope to apply MultiNest to the other data sets before the EPRV Evidence Challenge deadline, though happily I see that at least one other team has already applied MultiNest...