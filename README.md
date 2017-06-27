
<!-- README.md is generated from README.Rmd. Please edit that file -->
tipR: R tools for tipping point sensitivity analyses
====================================================

[![Build Status](https://travis-ci.org/LucyMcGowan/tipr.svg?branch=master)](https://travis-ci.org/LucyMcGowan/tipr)

**Authors:** [Lucy D'Agostino McGowan](http://www.lucymcgowan.com)<br/> **License:** [MIT](https://opensource.org/licenses/MIT)

Installation
------------

``` r
# install.packages(devtools)
devtools::install_github("lucymcgowan/tipr")
```

``` r
library("tipr")
```

Usage
-----

Enter estimated prevalences of an unmeasured confounder in the exposed and unexposed populations as well as the lower bound and upper bound of an effect you observe. The function will return the size of the unmeasured confounder needed to tip your analysis to non-significance.

``` r
tip_with_binary(p1 = 0.5, p0 = 0, lb = 1.2, ub = 1.3)
```

    ## [1] 1.4

If you are interested in outputting a single sentence for inclusion in a manuscript, use the `explanation = TRUE` option:

``` r
tip_with_binary(p1 = 0.5, p0 = 0, lb = 1.2, ub = 1.3, explanation = TRUE)
```

    ## An unmeasured confounder of size 1.4 with a prevalence of 0.5 in the 
    ## exposed population and 0 in the unexposed population would tip your 
    ## (1.2,1.3) result to nonsignificance.
