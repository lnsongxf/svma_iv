# Instrumental variable identification of dynamic variance decompositions

Matlab code for inference on variance decompositions and the degree of invertibility/recoverability in a general Structural Vector Moving Average (SVMA) model identified by external instruments (IVs)

**Reference:**
Plagborg-Møller, Mikkel and Christian K. Wolf (2020), "Instrumental Variable Identification of Dynamic Variance Decompositions", https://scholar.princeton.edu/mikkelpm/decomp_iv

Tested in: Matlab R2020a on Windows 10 PC (64-bit)

## Contents

**[functions](functions):** Matlab routines
- [SVMAIV_estim.m](functions/SVMAIV_estim.m): main function for SVMA-IV inference
- [SVARIV_estim.m](functions/SVARIV_estim.m): SVAR-IV inference (assumes invertibility)

**[application](application):** Empirical example
- [run_gk.m](application/run_gk.m): example based on Gertler & Karadi (2015)

**[illustration](illustration):** Numerical illustration
- [run_sw.m](illustration/run_sw.m): SVMA-IV and SVAR-IV analysis of Smets & Wouters (2007) model

**[simulations](simulations):** Simulation study

## Example

``` Matlab
addpath('functions');
% Given (T x n_y) data matrix Y with endogenous variables
% and (T x 1) data vector Z with external instrument
[bounds, id_recov] = ...
  SVMAIV_estim(Y, Z, ...
               'ic', 'aic', ...   % Select lag length using AIC
               'signif', 0.1, ... % 10% significance level
               'n_boot', 500, ... % 500 bootstrap iterations
               'horiz', 1:24);    % Compute horizons 1-24 of FVR/FVD
```
Output:
- `bounds` structure: partial identification bounds
  - `bounds.estim`: point estimates of bounds
  - `bounds.ci`: confidence intervals for identified set
- `id_recov` structure: results under additional assumption of recoverability
  - `id_recov.estim`: point estimates of parameters
  - `id_recov.ci`: confidence intervals for parameters

Parameter names:
- `alpha`: scale parameter
- `R2_inv`: degree of invertibility
- `R2_recov`: degree of recoverability
- `FVR`: forecast variance ratio
- `FVD`: forecast variance decomposition

See the [empirical application](application/run_gk.m) for a concrete example. Additional optional arguments to [`SMVAIV_estim.m`](functions/SVMAIV_estim.m) are listed at the top of the function.
