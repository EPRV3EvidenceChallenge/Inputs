# Notes for Ryan Cloutier's odds-ratio submission based on cross-validation

* Conversely to most (all?) other submitted techniques, cross-validation (CV) is not used to estimate the marginalized likelihood, instead it is used to estimate the predictive power of each model on previously unseen RV data


## Leave-one-out CV
* The dataset of N RV measurements is split into N unique train/test sets of N-1 and 1 RV measurement respectively. Each training set is equal to the full RV dataset less one measurement which itself constitutes the testing set
* On each training set, the parameters of each planet model are optimized
* The lnlikelihood (lnL) of measuring the unseen testing datum is then computed for each model using the optimized model parameters
* The sum of all N lnLs for each planet model are can then be compared (similarly to an odds ratio) to conclude which planet model is best suited to forecasting unseen measurements
* CV is a commonly used to avoid over-fitting of data as highly complex models can often be fine-tuned to provide a high likelihood whilst providing poor predictive power due to the finely-tuned parameters which do not necessarily generalize to unseen data (i.e. future observations)

## Time-Series Cross-Validation:
* Leave-one-out CV is applicable when measurements in the input dataset, which need not be a time-series, are uncorrelated. This is certainly not the case in an RV time-series whose adjacent points are highly correlated due to the presence of a periodic planetary signals and/or correlated noise arising from stellar activity
* When dealing with time-series, the removal of a single measurement does not remove all the information content associated with that datum due to correlations within the data
* As such we modify our method of train/test splitting of the data according to https://projecteuclid.org/euclid.ssu/1268143839 as described below
  * Given the full RV dataset of N measurements y_1,...,y_N, construct a training set of n0 measurements y_1,...,y_n0, where n0 < N is the smallest number of measurements required to optimize each models' parameters.
  * For this n=n0, optimize each models' parameters on the training set y_1,...,y_n0 and compute the lnL of the testing set y_(n0+1) for each model. In this way no future observations are used for training
  * Repeat the above steps of splitting, optimizing, and computing the lnL for n = n0,...,N-1
  * In this example the forecast is a singular value of length one since the testing set is the next chronological measurement following the last measurement in the training sample. Although, in principal, multiple forecast values could be used
* The results placed in the evidences_* files are the median lnliklelihood (lnL) per measurement because the lnL in each split is computed on the testing set which each contain a single measurement. The median lnL is desirable as there are known to be splits of the data wherein an optimal set of model parameters cannot be found. The median combination of each models' lnLs partially alleviates these poorly constrained models.
* The uncertainties on each model's median lnL per measurement are the median absolute deviations of the median lnL.
* The ratio of competing model median lnLs can be treated similarly to a Bayes factor and used for model comparison in this way. 
* Any questions regarding the methodology and how the results are used for model comparison should be directed to cloutier@astro.utoronto.ca

## Issues (RESOLVED)
* Model parameter optimizations in each split of the data are performed on a supercomputer to make the computation more tractable
* Recently, issues with the job submission procedure to that supercomputer have arised and so far prevented the calculation of results for RVdata0002.
* The source of this error is currently being investigated but may not be resolved before the deadline of September 14th.
