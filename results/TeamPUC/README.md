# Team PUC

Members: *J. Buchner & S. Rukdee*

We explore methods based on nested sampling. Our likelihood is implemented with george (Ambikasaran+14) and code adapted from ExoFit (Balan&Lahav08). To reduce the number of solutions, we impose ordering on the planet periods.

Nested sampling is an integration technique which explores the volume above a given likelihood threshold. That threshold is continuously increased, such that the volume decreases by a constant factor (exponential shrinkage). This allows nested sampling to keep track of the volume and likelihood value for making a Lebesgue integral. At a late point, the volume is small and the likelihood flat, so that the remainder does not contribute to the integral and the algorithm terminates.

The shrinkage of nested sampling is achieved by having e.g. 100 live points sampling the space and removing one. This reduces the represented volume by ~1/100. Next, the algorithm samples a new point with a likelihood higher than the removed point. The number of live points therefore determines the speed of the shrinkage and how coarsely the space is sampled.

The error of the integral estimate is given in Skilling09. The usual implementation (last formula) assumes that the bulk of the integral can be found around some shrinkage (rather than multiple). The formula is in practice a sufficient approximation.

Nested sampling internally requires an algorithm for drawing a new, random point from the prior with the condition that its likelihood is above the current likelihood threshold. Several general solutions for these constrained drawing algorithm exist, including those relying on local steps (MCMC, Galilean Monte Carlo, HMC, POLYCHORD) and those reconstructing the volume enclosed by the likelihood contour (MULTINEST, RADFRIENDS). See Buchner14 for a more detailed discussion. 

## MULTINEST

In this first version, we apply MULTINEST with several configurations.

The standard MULTINEST algorithm (Feroz+08) encloses the existing random points into best-fitting ellipsoids. These are enlarged by a certain factor (1/efficiency parameter). New points are drawn from the enlarged ellipsoids, and rejected if below the likelihood threshold. Therefore the ellipsoids reduce the space to be sampled, making MULTINEST fast. However, if the ellipsoids accidentally cut away parameter space regions (e.g. because the enlargement is too small or the contours do not look similar to ellipsoids), the estimate can be biased.

MULTINEST has two parameters, nlive (we chose 400) and efficiency (we chose 0.3).
The results can be found in 

* multinest-nlive400-eff0.3

## MULTINEST with Importance Nested Sampling

Importance Nested Sampling is a modification of Nested Sampling where the rejected points can improve the estimate (see Cameron&Pettitt13). This also mitigates issues of imperfect ellipsoid sampling mentioned above and was presented in Feroz+13.

We explore increasing the number of live points and decreasing the efficiency (for larger ellipsoids).
The results can be found in 

* multinest-ins-nlive400-eff0.3
* multinest-ins-nlive400-eff0.01
* multinest-ins-nlive2000-eff0.3



