# Vinesh Maguire-Rajpaul

## Algorithm overview

+ My results are obtained from a nested sampling implementation written in MATLAB, based heavily on code written by Pitkin & Romano, available [here](https://github.com/mattpitkin/matlabmultinest). 
+ The code uses the MCMC sampler from [Veitch & Veccio](https://arxiv.org/abs/0911.3820) to generate samples within a standard nested sampling routine. 
+ Note: this is *not* the same sampler as MultiNest by [Feroz, Hobson and Bridges](http://xxx.lanl.gov/abs/0809.3437), which is my usual go-to for evidence estimation. Given that another team has already obtained results using MultiNest, however, I didn't think it'd make sense for me to try to do the same. 
+ I used between 500 and 1500 live points (actual number randomly chosen prior to each MCMC run), $$N$$, with the number of MCMC elements, $$M$$, then fixed such that $$N \times M = 500,000$$, the latter number being chosen to make evidence estimation feasible in what seemed to me a reasonable length of time. M and N are as defined in the [Veitch & Veccio](https://arxiv.org/abs/0911.3820) paper.
+ For planet periods, I imposed the ordering $$P_1<P_2<P_3$$, rejecting samples that did not satisfy this criterion. I did not, however, perform any *post hoc* mode separation so e.g. it is possible/likely that even if only 1 planet is present in a data set, with RV semi-amplitude $$K_* $$, a 'bogus' three planet solution may be obtained where $$P_1\lesssim P_2 \lesssim P_3 $$ and $$K_1 \approx K_2 \approx K_3 \approx K_*/3 $$, with a similar situation for a 2-planet solution.
+ I estimated quantiles for $$\log_{10}Z$$ distribution via multiple runs of the above-described evidence calculation. In practice, however, given limited computational resources, "multiple" meant only $$\sim 5$$ MCMC runs per data set/model combination.

## General comments

+ For some reason my run times for 3-planet evidence estimation are shorter, on average, than for the 2-planet cases. No idea why.