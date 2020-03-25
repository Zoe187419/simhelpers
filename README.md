
<!-- README.md is generated from README.Rmd. Please edit that file -->

# simhelpers

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/meghapsimatrix/simhelpers.svg?branch=master)](https://travis-ci.org/meghapsimatrix/simhelpers)
[![Codecov test
coverage](https://codecov.io/gh/meghapsimatrix/simhelpers/branch/master/graph/badge.svg)](https://codecov.io/gh/meghapsimatrix/simhelpers?branch=master)
<!-- badges: end -->

Monte Carlo simulations are computer experiments designed to study the
performance of statistical methods under known data-generating
conditions (Morris, White, & Crowther, 2019). Methodologists use
simulations to examine questions such as: (1) how does ordinary least
squares regression perform if errors are heteroskedastic? (2) how does
the presence of missing data affect treatment effect estimates from a
propensity score analysis? (3) how does cluster robust variance
estimation perform when the number of clusters is small? To answer such
questions, we conduct experiments by simulating thousands of datasets
based on pseudo-random sampling, applying statistical methods, and
evaluating how well those statistical methods recover the true
data-generating conditions (Morris et al., 2019).

The goal of `simhelpers` is to assist in running simulation studies. The
main tools in the package consist of functions to calculate measures of
estimator performance like bias, root mean squared error, rejection
rates. The functions also calculate the associated Monte Carlo standard
errors (MCSE) of the performance measures. These functions are divided
into three major categories of performance criteria: absolute criteria,
relative criteria, and criteria to evaluate hypothesis testing. The
functions use the
[`tidyeval`](https://tidyeval.tidyverse.org/index.html) principles, so
that they play well with
[`dplyr`](https://dplyr.tidyverse.org/index.html) and fit easily into a
`%>%`-centric workflow (Wickham et al., 2019).

In addition to the set of functions that calculates performance measures
and MCSE, the package also includes a function, `create_skeleton()`,
that generates a skeleton outline for a simulation study. Another
function, `evaluate_by_row()`, runs the simulation for each combination
of conditions row by row. This function uses
[`future_pmap()`](https://davisvaughan.github.io/furrr/reference/future_map2.html)
from the [`furrr`](https://davisvaughan.github.io/furrr/) package,
making it easy to run the simulation in parallel. The package also
includes several datasets that contain results from example simulation
studies.

<img src="man/figures/workflow.png" />

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("meghapsimatrix/simhelpers")
```

## Related Work

Our explanation of MCSE formulas and our general simulation workflow is
closely aligned with the approach described by Morris et al. (2019). We
want to recognize several other R packages that offer functionality for
conducting Monte Carlo simulation studies. In particular, the
[`rsimsum`](https://cran.r-project.org/web/packages/rsimsum/index.html)
package (which has a lovely name that makes me hungry) also calculates
Monte Carlo standard errors (Gasparini, 2018). The
[`SimDesign`](https://cran.r-project.org/web/packages/SimDesign/index.html)
package implements a generate-analyze-summarize model for writing
simulations; it also includes tools for error handling and parallel
computing (Chalmers, 2019).

In contrast to the two packages mentioned above, our package uses
[`tidyeval`](https://tidyeval.tidyverse.org/index.html) and outputs
tibbles, which can then easily be used with
[`dplyr`](https://dplyr.tidyverse.org/index.html),
[`tidyr`](https://tidyr.tidyverse.org/) and
[`purrr`](https://purrr.tidyverse.org/) syntax. The functions that
calulate MCSEs are easy to run on grouped data. For parallel computing,
we use the [`furrr`](https://davisvaughan.github.io/furrr/) and
[`future`](https://rstudio.github.io/promises/articles/futures.html)
packages (Bengtsson, 2020; Vaughan & Dancho, 2018). Moreover, in
contrast to the `rsimsum` and `SimDesign` packages, `simhelpers`
provides jacknife MCSE for variance estimators. It also provides
jacknife MCSE estimates for root mean squared error.

Another related project is
[`DeclareDesign`](https://declaredesign.org/), a suite of packages that
allow users to declare and diagnose research designs, fabricate mock
data, and explore tradeoffs between different designs (Blair, Cooper,
Coppock, & Humphreys, 2019). This project follows a similar model for
how simulation studies are instantiated, but it uses a higher-level API,
which is tailored for simulating certain specific types of research
designs. In contrast, our package is a simpler set of general-purpose
utility functions.

Other packages that have similar aims to `simhelpers` include:
[MonteCarlo](https://cran.r-project.org/web/packages/MonteCarlo/index.html),
[parSim](https://cran.r-project.org/web/packages/parSim/index.html),
[simsalapar](https://cran.r-project.org/web/packages/simsalapar/index.html),
[simulator](https://cran.r-project.org/web/packages/simulator/index.html),
[simstudy](https://cran.r-project.org/web/packages/simstudy/index.html),
[simTool](https://cran.r-project.org/web/packages/simTool/index.html),
[simSummary](https://cran.r-project.org/web/packages/simSummary/index.html),
and [ezsim](https://cran.r-project.org/web/packages/ezsim/index.html).

# Acknowledgments

We are grateful for the feedback provided by [Sangdon
Lim](https://sdlim.com/) and Man Chen.

# References

<div id="refs" class="references">

<div id="ref-future">

Bengtsson, H. (2020). *Future: Unified parallel and distributed
processing in r for everyone*. Retrieved from
<https://CRAN.R-project.org/package=future>

</div>

<div id="ref-dd_2019">

Blair, G., Cooper, J., Coppock, A., & Humphreys, M. (2019). Declaring
and diagnosing research designs. *American Political Science Review*,
*113*(3), 838–859. Retrieved from <https://declaredesign.org/paper.pdf>

</div>

<div id="ref-SimDesign">

Chalmers, P. (2019). *SimDesign: Structure for organizing monte carlo
simulation designs*. Retrieved from
<https://CRAN.R-project.org/package=SimDesign>

</div>

<div id="ref-gasparini_2018">

Gasparini, A. (2018). Rsimsum: Summarise results from monte carlo
simulation studies. *Journal of Open Source Software*, *3*(26), 739.
<https://doi.org/10.21105/joss.00739>

</div>

<div id="ref-morris2019using">

Morris, T. P., White, I. R., & Crowther, M. J. (2019). Using simulation
studies to evaluate statistical methods. *Statistics in Medicine*,
*38*(11), 2074–2102.

</div>

<div id="ref-furrr">

Vaughan, D., & Dancho, M. (2018). *Furrr: Apply mapping functions in
parallel using futures*. Retrieved from
<https://CRAN.R-project.org/package=furrr>

</div>

<div id="ref-tidyverse">

Wickham, H., Averick, M., Bryan, J., Chang, W., McGowan, L. D.,
François, R., … Yutani, H. (2019). Welcome to the tidyverse. *Journal
of Open Source Software*, *4*(43), 1686.
<https://doi.org/10.21105/joss.01686>

</div>

</div>
