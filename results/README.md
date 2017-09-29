# Submissions to the Extremely Precise Radial Velocities 3:  Evidence Challenge

Results from the EPRV3 Evidence Challenge will go in subdirectories of this folder. 

### Working Draft Proposal for Directory Structure for Outputs
* Each team submitting results will be put results into their own subdirectory of the results folder in the https://github.com/EPRV3EvidenceChallenge/Inputs repository.  The directory name should begin with a letter and include only alphanumeric characters and underbars (e.g., Ford or Nelson_2016).
* Teams may submit results computed using multiple methods and/or assumptions as sub-subdirectories.  The directory names should begin with a letter and include only alphanumeric characters and underbars (e.g., AIC, LaplaceApproximation, RatioEstimator).  Please use a subdirectory with a meaningful name, even if you are only applying one method.  
* In the subfolder for each team-method, estimates of the evidences for each model (i.e., 0, 1, 2, and 3 planets) should be provided in one file per dataset, named evidences_0001a.txt, evidences_0002a.txt,..., evidences_0001b.txt, evidences_0002b.txt,... etc., where the number matches the number from the input dataset and the letter denotes whether it is based on the primary (board) periods priors ('a') or it is based on the alternative (narrowed) period priors ('b') (e.g., rvs_0001.txt -> evidences_0001a.txt and evidences_0001a.txt).  
* Alternatively, for methods that do not provide an estimate of the evidence, teams can submit a file with their estimates of the odds ratios comparing n-planet and (n+1)-planet models, in files named oddsratio_0001a.txt, oddsratio_0002a.txt, etc.
* In the subfolder for each team-method, benchmarking results for each model (i.e., 0, 1, 2, and 3 planets) should be provided in one file per dataset, named benchmarks_0001a.txt, benchmarks_0002a.txt, etc., where the number matches the number from the input dataset (e.g., rvs_0001.txt -> benchmarks_0001a.txt and benchmarks_0001b.txt) and the letter denotes the choice of prior.  
* Teams are encouraged but not required to submit estimates of key model parameters in a seprate file for each model, named params_0_0001a.txt, params_1_0001a.txt, etc., where the first number is the number of planets assumed and the second number matches the number from the input dataset (e.g., rvs_0001.txt assuming 2 planets -> params_2_0001.txt).  
* In the subfolder for each team-method, notes describing the method, assumptions, approximations, references, etc. are to go in a file named README.md .
* Teams are encouraged to submit results via git by creating a pull request containing their submissions.  If you're not comfortable with git, then we'll provide a place that you can upload a zip file.  

### Formats of Outputs: Evidences
* Comma delimited ASCII file (CSV)
* One row/line for each estimate of the evidence for each model (i.e., 0, 1, 2, and 3 planets) 
* Collumns:
  - A method-specific integer roughly perportional to how much computational effort was used (e.g., number of itterations, number of model evaluations, CPU-seconds; see details in specifications for files with evidence estimates).
     + Note that this is acting as a a label that allows one method to provide multiple estimates with more or less computational effort.  
     + Estimates for the evidence, all parameter values, and/or odds ratios should be provided with the same values/labels.
     + Nominal results for a given data set and model will be based on the entry with the largest value in this field.  Other results may be used to explore how rapidly a method is converging, but are unlikely to be explored during the EPRV3 meeting itself.
     + If you can not provide any estimate of computational effort for some method, then report 0 in the column.
  - How many planets were used for this line (a single integer)
  - Mode of estimated distribution for the log_10(evidence) (may be best point estimate)
  - Median of estimated distribution for the log_10(evidence) (may be same as mode)
  - Estimate for 2% percentile of the distribution for log_10(evidence) (analogous to "2-sigma lower")
  - Estimate for 16% percentile of the distribution for log_10(evidence) (analogous to "1-sigma lower")
  - Estimate for 84% percentile of the distribution for log_10(evidence) (analogous to "1-sigma higher")
  - Estimate for 98% percentile of the distribution for log_10(evidence) (analogous to "2-sigma higher")

### Formats of Outputs: Parameter Estimates
* Comma delimited ASCII file (CSV)
* One row/line for each estimate of a parameter within a given model (i.e., 0, 1, 2, and 3 planets)
* Collumns:
  - Method-specific integer roughly perportional to how much computational effort was used (e.g., number of itterations, number of model evaluations, CPU-seconds; see details in specifications for files with evidence estimates).
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
  
  
### Formats of Benchmarking Results
* Comma delimited ASCII file (CSV)
* One row/line for each estimate of the evidecne for each model (i.e., 0, 1, 2, and 3 planets) 
* Collumns:
  - Method-specific integer roughly perportional to how much computational effort was used; see details in specifications for files with evidence estimates).
  - How many planets were used for this line (a single integer)
  - number of evaluations of the full likelihood performed
  - number of evaluations of the gradient of the likelihood performed (probably 0 for most entries)
  - number of evaluations of the hessian of the likelihood performed (probably 0 for most entries)
  - number of matrix factorizations performed
  - number of evaluations of any other computationally significant part of your algorithm (e.g., large matrix inversions; probably 0 formost entries)
  - number of cores used (likely 1 for most entries)
  - wall clock time in seconds (only different if algorithm is parallelized)
* For benchmarking results, report NaN if number of evaluations and/or timing is not avaliable.  
* For algorithms that use only simple model evaluations, we suggest using ~10^5, 10^6, ... model evaluations for your evidence estimates.
* For more complex algorithms, you might try to adjust your parameters so that the computational cost is roughly equivalent to the number of core-seconds used by an algorithm with 10^5, 10^6, etc. simple model evaluations.  
* If people have codes that can be run in parallel easily, then it would be nice to report wall clock times for 1, 4, 8, and optionally 16 CPU-cores as separate lines, so we can see how the algorithm scales.  At least for now, it's probably sufficient to do this just for dataset 3, rather than for all the datasets.
* For the follow-up paper, we may ask you to rerun you existing analysis, adjusting the number of itterations/number of evaluations, so as to make the computational cost comparable to other entries.  


### Formats of Outputs: Odds Ratio
* Comma delimited ASCII file (CSV)
* One row/line for each estimate of the odds-ratio for a pair of models (e.g., 1-planet over 0-planet model, 2-planet over 1-planet model, ...)
   - Include comparisons of (n+1)-planet model to n-planet model, additional comparisons possible, but not necessary and may not be included in analysis
* Collumns:
  - Method-specific integer roughly perportional to how much computational effort was used (e.g., number of itterations, number of model evaluations, CPU-seconds; see details in specifications for files with evidence estimates).
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
  
### Formats of Additional Notes:
* README.md can be either ASCCI file (no unicode) or make use of [github Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).
* Begin with notes about the method in general.
* For notes particular to one particular dataset, place them in the above readme, using an "H3" section header with name "Dataset N", where N is the number of the dataset by placing 3 hashmarks at the beginning of the line.  E.g., ```### Dataset 1```.
* Otherwise, we can start with free form text.  If we see some common themes that are worth plotting, then we may ask for additional information to be standardize. 
  
