# Team PUC

Members: *J. Buchner & S. Rukdee*

We explore methods based on nested sampling. Our likelihood is implemented with george (Ambikasaran+14) and code adapted from ExoFit (Balan&Lahav08). To reduce the number of solutions, we impose ordering on the planet periods.

Nested sampling is an integration technique which explores the volume above a given likelihood threshold. That threshold is continuously increased, such that the volume decreases by a constant factor (exponential shrinkage). This allows nested sampling to keep track of the volume and likelihood value for making a Lebesgue integral. At a late point, the volume is small and the likelihood flat, so that the remainder does not contribute to the integral and the algorithm terminates.

The shrinkage of nested sampling is achieved by having e.g. 100 live points sampling the space and removing one. This reduces the represented volume by ~1/100. Next, the algorithm samples a new point with a likelihood higher than the removed point. The number of live points therefore determines the speed of the shrinkage and how coarsely the space is sampled.

The error of the integral estimate is given in Skilling09. The usual implementation (last formula) assumes that the bulk of the integral can be found around some shrinkage (rather than multiple). The formula is in practice a sufficient approximation.

Nested sampling internally requires an algorithm for drawing a new, random point from the prior with the condition that its likelihood is above the current likelihood threshold. Several general solutions for these constrained drawing algorithm exist, including those relying on local steps (MCMC, Galilean Monte Carlo, HMC, POLYCHORD) and those reconstructing the volume enclosed by the likelihood contour (MULTINEST, RADFRIENDS). See Buchner14 for a more detailed discussion. 

## MULTINEST

We apply MULTINEST with several configurations.

The standard MULTINEST algorithm (Feroz+08) encloses the existing random points into best-fitting ellipsoids. These are enlarged by a certain factor (1/efficiency parameter). New points are drawn from the enlarged ellipsoids, and rejected if below the likelihood threshold. Therefore the ellipsoids reduce the space to be sampled, making MULTINEST fast. However, if the ellipsoids accidentally cut away parameter space regions (e.g. because the enlargement is too small or the contours do not look similar to ellipsoids), the estimate can be biased.

MULTINEST has two parameters, nlive and efficiency (inverse of ellipse enlargement). We chose a standard configuration and two variations, increasing either the number of live points or the enlargement. The results can be found in 

* multinest-nlive400-eff0.3
* multinest-nlive400-eff0.01
* multinest-nlive2000-eff0.3

## MULTINEST with Importance Nested Sampling

Importance Nested Sampling is a modification of Nested Sampling where the rejected points can improve the estimate (see Cameron&Pettitt13). This also mitigates issues of imperfect ellipsoid sampling mentioned above and was presented in Feroz+13. MULTINEST computes both the standard nested sampling estimator and the importance nested sampling estimator, so we also submit the latter, for the same runs.

The results can be found in 

* multinest-ins-nlive400-eff0.3
* multinest-ins-nlive400-eff0.01
* multinest-ins-nlive2000-eff0.3


## Multiple MULTINEST runs

We observe that there is substantial scatter and outliers in the evidences, particularly in data sets 4,5 and 6. This can come from e.g. undiscovered solutions and imperfect ellipsoids. We therefore also include results where we run MULTINEST 6 times and combine the evidence estimates (logZ=median of the logZi's and logZerr=sqrt(median(Zerrs)^2, median(|logZi-logZ|)^2)). This avoids the influence of outliers but gives appropriate errors for the scatter when MULTINEST is having trouble.

A conclusion from this work is that running MULTINEST once is probably not enough to be sure of its evidence values, and that an efficiency of 0.3 is too high (and can not be remedied by increasing the number of live points).

* multirun-multinest-nlive400-eff0.3
* multirun-multinest-nlive400-eff0.01
* multirun-multinest-nlive2000-eff0.3
* multirun-multinest-ins-nlive400-eff0.3
* multirun-multinest-ins-nlive400-eff0.01
* multirun-multinest-ins-nlive2000-eff0.3


## Importance Sampling

This technique is not based on nested sampling, but on variational Bayes and Importance Sampling
to perform the integration.

We used the pypmc package (https://zenodo.org/badge/latestdoi/15123/fredRos/pypmc) and the technique described in Beaujean&Caldwell13.

In detail the technique is as follows:

* Step 1: Identify likelihood maxima. The original technique used several MCMC chains, here I re-used a single multinest run to obtain initial posterior points. This just serves to identify a initial mixture density and does not rely on multinest sampling correctly.
* Step 2: Generate an initial proposal mixture density from the chains (make_r_gaussmix). 
* Step 3: Run Variational Bayes to optimize the proposal mixture density
* Step 4: Create a Importance Sampler. Set N=n_params*1000.
* Step 5: Loop, incrementing i from 0:
  * draw N importance samples.
  * If integral uncertainty is below the threshold deltalnZ~0.8 and the effective sampling size is above 100, terminate.
  * Otherwise: Increase N by 1.4 (samples drawn increases exponentially)
  * Update the proposal mixture density with Variational Bayes
  * If i mod 3 is 2 (i.e. every third loop), the previous is not done. Instead, the proposal mixture density is recreated from scratch, but with one more MCMC chain. That MCMC chain is started from the point with the highest weight, after a simple optimization step. 

A problem with applying Variational Bayes iteratively to improve the effective sample size is that the number of components can not increase. So if a new small peak is discovered, VB typically does not place a component there. To solve these two problems, we recreate the mixture from scratch (with up to 10 components). The local MCMC run helps identifying the size of the possible new component. In the subsequent iteration, *all* previous samples are used to optimized the mixture, and the number of components can shrink drastically again.

The technique could still be optimized. For example, Step 1 could be replaced by another global search technique (Differential evolution, or multiple MCMC chains) to be less cost-intensive than MULTINEST. However, the current setup seems to work OK.

Our total number of likelihood evaluations include the MULTINEST prerun (multinest-ins-nlive400-eff0.3). The Variational Bayes cost is quite small compared to the likelihood evaluations.

These results can be found in:

* vb-importance-sampling

Finally, we include a long version of this algorithm, where we combine 10 MULTINEST preruns, higher number of samples, and integrate to a higher effective sampling size (20000) before terminating. At the cost of many likelihood evaluations, this should be safer.

* vb-importance-sampling-long

For some data sets, this stringent termination criterion was not reached and the runs were terminated manually.



