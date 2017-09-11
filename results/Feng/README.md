# Notes for Fabo Feng's result
## BIC and Chib's method

### Method I: BIC
The evidence is approximated by using evidence=e^(-BIC/2) and BIC=-2*ln(L_max)+k*ln(N),where L_
max is the maximum likelihood,
k is the number of free parameters, and N is the number of data points. The maximum likelihood 
is calculated throuhg posterior
sampling implemented using DRAM, an adaptive MCMC algorithm, see [Haario, Saksman & Tamminen 20
01](https://projecteuclid.org/euclid.bj/1080222083).
The BIC estimator is not expected to estimate evidence accurately. Rather it is used to calcula
te
the Bayes factor (BF) or evidence ratio such that a threhold can be applied to select planetary
 signals (see [Feng et al. 2016, MNRAS](https://arxiv.org/abs/1606.05196)).
In Feng et al. 2016, MNRAS, we have also investigated other estimators of BF such as AIC, DIC, 
truncated posterior mixture (TPM) by Tuomi & Jones 2012, and the Chib's method (Chib & Jeliazko
v 2001),
and find that the BIC and Chib's methods are optimal and are conservative enough to select Kepl
erian signals. To estimate the uncertainty of BIC-estimation evidence, I have
divided the MCMC posterior samples into 100 subsamples, and calcualte the evidence for each.

### Method II: Chib's method
Unlike other methods, the Chib's method ([Chib & Jeliazkov 2001](http://www2.stat.duke.edu/~scs
/Courses/Stat376/Papers/NormConstants/ChibMHJASA2001.pdf)) is to calculate the evidence as a no
rmalization constant of the posterior density of certain points in the
parameter space. Specifically, the Chib’s method is based on the calculation of the posterior o
f a single point using samples drawn from the posterior
density and the proposal density of a Metropolis–Hastings sampler (or Gibbs sampler). The param
eter vector can be partitioned into arbitrary
numbers of blocks. I only apply the one-block sampling (Eqn. 9 and 10) introduced in Chib & Jel
iazkov 2001. I have used 10^4 MCMC posterior samples
to calulate the posterior density of a given point. Then I repeat this step 100 times to get th
e mean, mode and quantiles of the distribution
of evidence.