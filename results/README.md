# Submissions to the Extremely Precise Radial Velocities 3:  Evidence Challenge

Results from the EPRV3 Evidence Challenge will go in subdirectories of this folder. 
We have yet to finalize the specificaitons for how to submit results.  
I've drafted a preliminary plan below, and encourage participants to provide feedback and offer suggestions up until we finalize the output formats.

### Working Draft Proposal for Directory Structure for Outputs
* Each team submitting results will be put results into their own subdirectory of the results folder in the https://github.com/EPRV3EvidenceChallenge/Inputs repository.  The directory name should begin with a letter and include only alphanumeric characters and underbars (e.g., Ford or Nelson_2016).
* Teams may submit results computed using multiple methods and/or assumptions as sub-subdirectories.  The directory names should begin with a letter and include only alphanumeric characters and underbars (e.g., AIC, LaplaceApproximation, RatioEstimator).  Please use a subdirectory with a meaningful name, even if you are only applying one method.  
* In the subfolder for each team-method, estimates of the evidences for each model (i.e., 0, 1, 2, and 3 planets) should be provided in one file per dataset, named evidences_0001.txt, evidences_0002.txt, etc., where the number matches the number from the input dataset (e.g., rvs_0001.txt -> evidences_0001.txt).  
* Alternatively, for methods that do not provide an estimate of the evidence, teams can submit a file with their estimates of the odds ratios comparing n-planet and (n+1)-planet models, in files named oddsratio_0001.txt, oddsratio_0002.txt, etc.
* Teams are encouraged but not required to submit estimates of key model parameters in a seprate file for each model, named params_0_0001.txt, params_1_0001.txt, etc., where the first number is the number of planets assumed and the second number matches the number from the input dataset (e.g., rvs_0001.txt assuming 2 planets -> params_2_0001.txt).  
* Teams are encouraged to submit results via git by creating a pull request containing their submissions.  If you're not comfortable with git, then we'll provide a place that you can upload a zip file.  

### Working Draft Proposal for Formats of Outputs: Evidences
* Comma delimited ASCII file (CSV)
* One row/line per model (i.e., 0, 1, 2, and 3 planets)
* Collumns:
  - How many planets were used for this line (a single integer)
  - Mode of estimated distribution for the log_10(evidence) (may be best point estimate)
  - Median of estimated distribution for the log_10(evidence) (may be same as mode)
  - Estimate for 2% percentile of the distribution for log_10(evidence) (analogous to "2-sigma lower")
  - Estimate for 16% percentile of the distribution for log_10(evidence) (analogous to "1-sigma lower")
  - Estimate for 84% percentile of the distribution for log_10(evidence) (analogous to "1-sigma higher")
  - Estimate for 98% percentile of the distribution for log_10(evidence) (analogous to "2-sigma higher")

### Working Draft Proposal for Formats of Outputs: Parameter Estimates
* Comma delimited ASCII file (CSV)
* One row/line per parameter and model (i.e., 0, 1, 2, and 3 planets)
* Collumns:
  - Letter indicating which parameter is being estimated.  Options are:
      + P: Orbital Period
      + K: RV Amplitude
      + h: h=e*sin(omega), where e is eccentricity & omega is arguement of periastron 
      + k: k=e*cos(omega)
      + l: l=omega+M:  The sum of the argument of pericenter and the mean anomaly at epoch t=300 days.  (We realize that different groups parameterize this differently, so we anticipate that not all groups will submit estimates for this parameter.)
      + C: The radial velocity offset, i.e., star velocity if all amplitudes were 0.
      + J: \sigma_j, the amplitude of additional white-noise, often casually referred to as ``jitter''
  - How many planets were used for this line (a single integer).
  - Index of planet whose parameters are given on this line (a single integer).  
      + Label inner-most planet detected (for model with the given number of planets) as 1
      + Planet indices increase with orbital period
      + Use 0 for parameters that are characteristic of the system rather than one planet (e.g., RV offset and \sigma_j)
  - Mode of estimated distribution for this line's parameter (may be best point estimate)
  - Median of estimated distribution for this line's parameter (may be same as mode)
  - Estimate for 2% percentile of the distribution for this line's parameter (analogous to "2-sigma lower")
  - Estimate for 16% percentile of the distribution for this line's parameter (analogous to "1-sigma lower")
  - Estimate for 84% percentile of the distribution for this line's parameter (analogous to "1-sigma higher")
  - Estimate for 98% percentile of the distribution for this line's parameter (analogous to "2-sigma higher")
  
  
### Working Draft Proposal for Formats of Outputs: Odds Ratio
* Comma delimited ASCII file (CSV)
* One row/line per odds-ratio (e.g., 1-planet over 0-planet model, 2-planet over 1-planet model, ...)
   - Include comparisons of (n+1)-planet model to n-planet model, additional comparisons possible, but not necessary and may not be included in analysis
* Collumns:
  - number of planets in model for denominator of odds ratio (a single integer)
  - number of planets in model for numerator of odds ratio (a single integer)
  - Mode of estimated distribution for the log_10(odds ratio) (may be best point estimate)
  - Median of estimated distribution for the log_10(odds ratio) (may be same as mode)
  - Estimate for 2% percentile of the distribution for log_10(odds ratio) (analogous to "2-sigma lower")
  - Estimate for 16% percentile of the distribution for log_10(odds ratio) (analogous to "1-sigma lower")
  - Estimate for 84% percentile of the distribution for log_10(odds ratio) (analogous to "1-sigma higher")
  - Estimate for 98% percentile of the distribution for log_10(odds ratio) (analogous to "2-sigma higher")
* Questions for groups likely to submit estimates of odds ratios.  
  - Is this too much?  If so, how do you propose to submit both an odds-ratio and some measure of uncertainty?
  
