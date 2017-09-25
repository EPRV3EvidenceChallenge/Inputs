# Notes for Eric Ford's submission to the EPRV3 Evidence Challenge

## Method 1 (laplace_linearized_circ):
* We model the RV signal is a superposition of sinusoidal signals at the planet orbital periods (i.e., no harmonics)
* We perform brute force integraion over orbital period (with an ovesampling parameter of 8 or 32, when searching all periods or a narrow range, respectively)
* We perform Gauss-Legendre quadrature to integrate over the parameter log(1+sigma_j/sigma_{j,o}) using 40 nodes.
* We write the model for the remaining parameters in terms of amplitudes, so it becomes linear in those parameters.
* Computational effort was reported as seconds (rounded up) on a single core of a laptop.
* Search for a first plane, respectivelyt
  * Find best-fit amplitudes and Fischer information matrix for each period and sigma_j considered.
  * Approximate integrals over linear parameters via the Laplace approximation (i.e., extending limits to infinity, remembering to include Jacobian for change of variables) 
  * Find largest peak in the resulting profile log posterior over orbital period (like a "Bayesian periodogram")
  * Perform non-linear optimization over period(s)
  * Update best-fit parameters, best-fit, Hessian and Laplace approximation to the log marginal posterior at optimized period(s)
  * If the log marginal posterior from the one peak is greater than the brute force integral over periods, report the updated Laplace approximation as the marginalized log posterior.  
  * Otherwise, report the brute force sum based on the original Laplace approximations to the marginal log posterior conditioned on each period
* Search for a second/third planet
  * Perform new brute force integraion over orbital period of the second/third planet, while excluding periods within a factor of 1.15 of previously identified planets (only when searching the full period range) and holding their periods fixed at previous values (after optimization)
  * Find largest peak in the resulting profile log posterior over orbital period of the new planet
  * Perform non-linear optimization over period(s)
  * Update best-fit parameters, best-fit, Hessian and Laplace approximation to the log marginal posterior at optimized period(s)
  * If the log marginal posterior from the one peak is greater than the brute force integral over periods, report the updated Laplace approximation as the marginalized log posterior.  
  * Otherwise, report the brute force sum based on the original Laplace approximations to the marginal log posterior conditioned on each period


## Method 2 (laplace_linearized_ecc): 
* Similar to Method 1, except we include the first harmonic for each planet (i.e., epicycle approximation)
* First, use brute force integration using the circular model from Method 1
* Refit the RV model including a first harmonic for each planet
* Test what fraction of samples have eccentricities < 1.  
* Currently, add eccentricities "all-at-once", rather than one-at-a-time.

## Method 3 (laplace_keplerian):
* Similar to methods 1 and 2, except we use a linear superposition of Keplerian orbits for the RV model
* First, use estimated orbital periods and sigma_j from outputs of Method 2
* Technically, am using phases, but I don't think I've coded it right, so for now, it's researching over phases and omega within the Keplerian model
* Optimize all model parameteres except sigma_j.  
* Evaluate Fischer Information Matrix at local mode and compute Laplace approximation to the log marginal posterior.
* Note that for now, we used Laplace approximation to marginalize over sigma_j, rather than the more accurate Gauss-Legendre method that was used in Methods 2 and 3. (This is just due to bug in scripts.) 


## Notes
* As we go from method 1 to method 3, we are using a more accurate approximation of the RV model.  In theory, this would allow for more accurate estimates of the marginalized posterior.  However, the increased model complexity also means that the processes for identifying the global mode become less robust.  Thus, there is an increased risk of a result that deviates significantly from it the true global mode had been identified.  
* I suspect that the algorithms probably work quite well for readily detectable planets, since the marginalized posterior is very likely dominated by a single mode. 
* However, I anticipate that the method 3 will give inaccurate results when there are weak detections or non-detections, since multiple modes are likely to contribute significantly to the marginalized posterior in such cases.
* The results submitted were all computed automatically, without any human help in identifying or deciding between local maximum, deciding if the fit was any good, or even looking at the dataset.  Obviously, one would want to look at the data and perform some form of model evaluation before presenting results for any real science application.  
* The heuristics for finding the global mode were not based on a mature pipeline, but written just for this test in a couple of days.  Thus, they are not mature and may be succeptible to missing the global mode.  I suspect that any significantly spurious results of the Keplerian model could be corrected with either a little human help or more robust algorithm for choosing the starting parameters for the optimizer.  

