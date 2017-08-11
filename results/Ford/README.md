# Notes for Eric Ford's submission to the EPRV3 Evidence Challenge

## Method 1 (laplace_linearized_circ):
* We model the RV signal is a superposition of sinusoidal signals at the planet orbital periods (i.e., no harmonics)
* We perform brute force integraion over orbital period (with an ovesampling parameter of 4)
* We perform Gauss-Legendre quadrature to integrate over the parameter log(1+sigma_j/sigma_{j,o}) using 40 nodes.
* We write the model for the remaining parameters in terms of amplitudes, so it becomes linear in those parameters.
* Computational effort was reported as seconds (rounded up) on a single core of a laptop.
* Search for a first planet
  * Find best-fit amplitudes and Fischer information matrix for each period and sigma_j considered.
  * Approximate integrals over linear parameters via the Laplace approximation (i.e., extending limits to infinity, remembering to include Jacobian for change of variables) 
  * Find largest peak in the resulting profile log posterior over orbital period (like a "Bayesian periodogram")
  * Perform non-linear optimization over period(s)
  * Update best-fit parameters, best-fit, Hessian and Laplace approximation to the log marginal posterior at optimized period(s)
  * If the log marginal posterior from the one peak is greater than the brute force integral over periods, report the updated Laplace approximation as the marginalized log posterior.  
  * Otherwise, report the brute force sum based on the original Laplace approximations to the marginal log posterior conditioned on each period
* Search for a second/third planet
  * Perform new brute force integraion over orbital period of the second/third planet, while excluding periods within a factor of 1.2 of previously identified planets and holding their periods fixed at previous values (after optimization)
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


