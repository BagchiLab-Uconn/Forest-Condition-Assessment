# Forest Condition Assessment
An accompanying code and data repository for the paper Pasquarella, V.J., Mickley, J.G., Barker Plotkin, A., MacLean, R. G., Anderson, R. M., Brown, L. M., Wagner, D. L., Singer, M. S., &amp; Bagchi, R. (2021). Predicting defoliator abundance and defoliation measurements using Landsat-based condition scores. *Remote Sensing in Ecology and Conservation*. [https://doi.org/10.1002/rse2.211](https://doi.org/10.1002/rse2.211)

Here, we compare the relative predictive ability of various parameterizations of remote-sensed forest condition assessments on abundance and damage from a *Lymantria dispar* outbreak in southern New England. 

#### Instructions:
* Data files should be stored inside the [data](data/) directory.
* Scripts for Earth Engine workflow are stored in the [earthengine_workflow](earthengine_workflow/) directory and the repository can be accessed on Earth Engine [here](https://code.earthengine.google.com/?accept_repo=users/valeriepasquarella/harmonic_baseline_experiments).
* Analyses should be stored in the [analyses](analyses/) directory.
* Use the [analysis template](analyses/Analysis-Template.Rmd) in analyses/ as a starting point.

#### List of Analyses:
* [Defoliation Models](analyses/Defoliation-Models.md) - Comparison of defoliation models for forest condition assessment
* [Using AIC weights to pick a winner](analyses/AIC_weights.md) - Can AIC model weights be used to pick a consensus best model parameterization?

#### Harmonic baseline results:
* Results can be viewed interactively via an [Earth Engine App](https://valeriepasquarella.users.earthengine.app/view/harmonic-baseline-experiments)
* Mapped results are available as a [Zenodo dataset](https://doi.org/10.5281/zenodo.4825877)

