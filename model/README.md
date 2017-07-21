# Model description
Input Data &amp; Model for the EPRV3 Evidence Challenge - Start Here

The full specifications for the model and choices of priors are given in model.tex and model.pdf .

Note that In responce to suggestions from Joao, Ryan, and Vinesh, we updated the priors to be used for the EPRV3 challenge on 7/20/2017.
- The prior for the RV offset is now uniform over a finite range, p(C) dC = dC/(2C_max) for -C_max<C<C_max, C_max = 10^3 m/s.
- The prior for orbital period is now p(P) dP = dP/P * (1/ln(P_max/P_min)), with P_min = 1 day and P_max=10^4 days (and zero when P is outside this range).
- The expressions for priors for RV amplitude and magnitude of the white noise term were corrected to be properly normalized.  (I had left out a factor of 1m/s.)  
- We clarified that the priors for RV amplitude and magnitude of the white noise term are non-zero for all positive RV amplitudes and sigma_J's, i.e., going all the way to zero.  
- We clarified that log's are base e.
