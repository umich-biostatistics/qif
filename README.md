
<!-- README.md is generated from README.Rmd. Please edit that file -->

# qif

<!-- badges: start -->

<!-- badges: end -->

## Quadratic Inference Function fit of balanced longitudinal data

## Installation

You can install the released version of qif from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("qif")
```

Or install the development version from
[Github](https://github.com/umich-biostatistics/FEprovideR)
with:

``` r
install.packages("devtools") # you need devtools to install packages from Github
devtools::install_github("umich-biostatistics/qif")
```

## Examples

``` r
## Marginal log-linear model for the epileptic seizures count data
## (Diggle et al., 2002, Analysis of Longitudinal Data, 2nd Ed., Oxford Press).

# Read in the epilepsy data set:
data(epil)

# Fit the QIF model:
fit <- qif(y ~ base + trt + lage + V4, id=subject, data=epil,
                                       family=poisson, corstr="AR-1")
 
# Alternately, use ginv() from package MASS
fit <- qif(y ~ base + trt + lage + V4, id=subject, data=epil,
                      family=poisson, corstr="AR-1", invfun = "ginv")


# Print summary of QIF fit:
summary(fit)


## Second example: MS study
data(exacerb)

qif_BIN_IND<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="independence")
                        
qif_BIN_AR1<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="AR-1")
                        
qif_BIN_CS<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="exchangeable")
                        
qif_BIN_UN<-qif(exacerbation ~ treatment + time + duration + time2, id=id,
                        data=exacerb, family=binomial, corstr="unstructured")

summary(qif_BIN_CS)

qif_BIN_CS$statistics

qif_BIN_CS$covariance
```
