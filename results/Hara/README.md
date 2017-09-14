# Notes for Nathan Hara's submission to the EPRV3 Evidence Challenge

## Method 1 (l1 periodogram):
* The folder 'l1_periodrogram' contains the plots obtained with the method described in my phd thesis (same as Hara, Boué, Laskar & Correia 2017 with minor changes)
* The method consists in solving  arg min ||x||_l1 subject to || Ax - y||_l2 <= epsilon where y is the 200 measurements data set, A is a 200 times 40,000 matrix A_kl = exp(+/- i omega_l t_k) plus some steps described in Hara, Boué, Laskar & Correia 2017. (omega_l)_l=1..20,000 is an equispaced array of frequencies spanning from 0 to 2pi/1.25. 
* On each plot we consider the three principal peaks. The False alarm probabilities (FAP) are reported as follows

* We compute Z1 = 0.5*N (chi2(model with j+1 planets) - chi2(model with j planets)) / chi2(model with j planets) where the chi2(model with j planets) is the chi square of the residuals of j sine functions and a constant fitted non linearly. The covariance matrix given in the document describing the model (quasi periodic Kernel). We take N = 200 - 3*j - 1, that is the number of measurements minus the number of degrees of freedom of the model with j planets.
* The FAP corresponds to Probability(Z> Z1 | model with j planets), as given by equation 2 and 5 in Baluev 2008. Z is the random variable 'maximum of the periodogram on the frequency grid' under the hypothesis 
* We report the logarithm in base 10 of the FAP

* We report periods with a precision of four digits, which correspond to the maxima of the l1 periodogram, we obviously do not have such a resolution in general. 
