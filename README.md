
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

After fitting your model, you can determine the unmeasured confounder needed to tip your analysis. This unmeasured confounder is determined by two quantities, the association between the exposure and the unmeasured confounder `rr_eu`, and the association between the unmeasured confounder and outcome `rr_ud`. Using the `tip_mod()` function, we can fix one of these and solve for the other. Alternatively, we can fix both and solve for `n`, that is, how many unmeasured confounders of this magnitude would tip the analysis. We can also leave both blank and solve for the minimum joint association, put forth by VanderWeele and Ding, known as the E-value.

``` r
## Fit a model
mod <- glm(vs ~ mpg, data = mtcars, family = binomial())
```

Solve for the association between the exposure and unmeasured confounder needed to tip the analysis.

``` r
mod %>%
  tip_mod(exposure = "mpg",
      rr_ud = 1.4)
```

    ## # A tibble: 1 x 5
    ##         lb       ub    rr_eu rr_ud     n
    ##      <dbl>    <dbl>    <dbl> <dbl> <dbl>
    ## 1 1.203144 2.280633 2.444723   1.4     1

Solve for the association between the unmeasured confounder and the outcome needed to tip the analysis.

``` r
mod %>%
  tip_mod(exposure = "mpg",
      rr_eu = 1.4)
```

    ## # A tibble: 1 x 5
    ##         lb       ub rr_eu    rr_ud     n
    ##      <dbl>    <dbl> <dbl>    <dbl> <dbl>
    ## 1 1.203144 2.280633   1.4 2.444723     1

Solve for the minimum joint association between the exposure and unmeasured confounder and the unmeasured confounder and outcome, also known as the E-value.

``` r
mod %>%
   tip_mod(exposure = "mpg")
```

    ## # A tibble: 1 x 5
    ##         lb       ub    rr_eu    rr_ud     n
    ##      <dbl>    <dbl>    <dbl>    <dbl> <dbl>
    ## 1 1.203144 2.280633 1.697525 1.697525     1
