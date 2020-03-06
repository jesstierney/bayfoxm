# bayfoxm

A Bayesian, global planktic foraminifera core top calibration to sea-surface temperature (SST), for MATLAB.

## What is BAYFOX?

BAYFOX is a suite of linear Bayesian calibration models for planktic core top foraminiferal &delta;<sup>18</sup>O (&delta;<sup>18</sup>O<sub>c</sub>) and SSTs. These calibrations are especially useful because they capture the uncertainty in the relationship between modern SSTs and core top δ18Oc. This package is a companion to a paper published in the journal "Paleoceanography and Paleoclimatology":

Malevich, S. B., Vetter, L., & Tierney, J. E. (2019). Global Core Top Calibration of &delta;<sup>18</sup>O in Planktic Foraminifera to Sea Surface Temperature. Paleoceanography and Paleoclimatology, 34(8), 1292-1315.

Please cite this paper when using BAYFOX.

The BAYFOX calibration are also available in the [`bayfox` package](https://github.com/brews/bayfox) for Python, and the [`bayfoxr` package](https://github.com/brews/bayfoxr) for the R statistical environment. This MATLAB version of bayfox has been optimized by J. Tierney to accept arguments that are similar in style to those associated with the other Bayesian models we have developed (BAYMAG, BAYSPLINE, BAYSPAR).

## A quick guide to use:

To model &delta;<sup>18</sup>O<sub>c</sub> from SST and &delta;<sup>18</sup>O<sub>sw</sub>:

Use `bayfox_forward.m`. This function calculates &delta;<sup>18</sup>O<sub>c</sub> values using posterior draws from the calibration model (stored in the params.mat files). bayfox_forward has no dependent functions but does need the params.mat files. You must use input one of the designated options for the species of foraminifera. An example call would be:

d18oc = bayfox_forward(t,d18osw,'ruber');

The output is a 1000-member ensemble of &delta;<sup>18</sup>O<sub>c</sub> values.

To model SST from &delta;<sup>18</sup>O<sub>c</sub>:

Use `bayfox_predict.m`. This function inverts the calibration model to predict SSTs from foraminiferal &delta;<sup>18</sup>O<sub>c</sub>. The user must input &delta;<sup>18</sup>O<sub>sw</sub> along with a prior mean and standard deviation (in degrees C), which can be either scalars or vectors. Here is a typical call:

output = bayfox_predict(d18oc,d18osw,prior_mean,prior_std,species,bayes);

The output here is a structure which records the prior mean and standard deviation, the 2.5%, 50%, and 97.5% confidence intervals of SST, and the full posterior ensemble of SST.


