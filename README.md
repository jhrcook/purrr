
<!-- README.md is generated from README.Rmd. Please edit that file -->

# purrr <img src="man/figures/logo.png" align="right" />

[![CRAN\_Status\_Badge](https://www.r-pkg.org/badges/version/purrr)](https://cran.r-project.org/package=purrr)
[![Build
Status](https://travis-ci.org/tidyverse/purrr.svg?branch=master)](https://travis-ci.org/tidyverse/purrr)
[![AppVeyor Build
Status](https://ci.appveyor.com/api/projects/status/github/tidyverse/purrr?branch=master&svg=true)](https://ci.appveyor.com/project/tidyverse/purrr)
[![Coverage
Status](https://img.shields.io/codecov/c/github/tidyverse/purrr/master.svg)](https://codecov.io/github/tidyverse/purrr?branch=master)

## Overview

purrr enhances R’s functional programming (FP) toolkit by providing a
complete and consistent set of tools for working with functions and
vectors. If you’ve never heard of FP before, the best place to start is
the family of `map()` functions which allow you to replace many for
loops with code that is both more succinct and easier to read. The best
place to learn about the `map()` functions is the [iteration
chapter](http://r4ds.had.co.nz/iteration.html) in R for data science.

## Installation

``` r
# The easiest way to get purrr is to install the whole tidyverse:
install.packages("tidyverse")

# Alternatively, install just purrr:
install.packages("purrr")

# Or the the development version from GitHub:
# install.packages("devtools")
devtools::install_github("tidyverse/purrr")
```

## Cheatsheet

<a href="https://github.com/rstudio/cheatsheets/blob/master/purrr.pdf"><img src="https://raw.githubusercontent.com/rstudio/cheatsheets/master/pngs/thumbnails/purrr-cheatsheet-thumbs.png" width="630" height="252"/></a>

## Usage

The following example uses purrr to solve a fairly realistic problem:
split a data frame into pieces, fit a model to each piece, compute the
summary, then extract the R<sup>2</sup>.

``` r
library(purrr)

mtcars %>%
  split(.$cyl) %>% # from base R
  map(~ lm(mpg ~ wt, data = .)) %>%
  map(summary) %>%
  map_dbl("r.squared")
#>         4         6         8 
#> 0.5086326 0.4645102 0.4229655
```

This example illustrates some of the advantages of purrr functions over
the equivalents in base R:

  - The first argument is always the data, so purrr works naturally with
    the pipe.

  - All purrr functions are type-stable. They always return the
    advertised output type (`map()` returns lists; `map_dbl()` returns
    double vectors), or they throw an error.

  - All `map()` functions either accept function, formulas (used for
    succinctly generating anonymous functions), a character vector (used
    to extract components by name), or a numeric vector (used to extract
    by position).

-----

Please note that this project is released with a [Contributor Code of
Conduct](https://purrr.tidyverse.org/CODE_OF_CONDUCT). By participating in this project you agree
to abide by its terms.
