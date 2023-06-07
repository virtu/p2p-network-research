# Research on eclipse attacks

Research on the impact of ASMAP, including analytic modeling of eclipse attacks and
increased cost for attackers.

## Overview

- `01_prep_input_data.ipynb`: Annotate node IP addresses data (provided in
  `reachable-nodes-2023-05-07.csv`) with netgroup and ASN data (ASN data is taken from
  `asmap-kartograf-2023-02-06.txt.bz2`, which was generated
  using [kartograf](https://github.com/fjahr/kartograf/tree/master/kartograf), and store
  results.
- `02_empirical_data.ipynb`: Netgroup and ASN distribution plots.
- `03_prefix_asn_mapping_sim.ipynb`: Monte Carlo-based analysis of netgroup-ASN mapping.
- `04_model_validation.ipynb`: Empirical validation of analytic model, modeling insights
  and performance optimizations. Necessary steps to run the analytic model up are
  documented in [probabilities for multivariate noncentral
  Wallenius distribution](#probabilities-for-multivariate-noncentral-wallenius-hypergeometric-distribution)
- `05_eclipse_probabilities.ipynb`: modeling of eclipse probabilities

## Probabilities for multivariate noncentral Wallenius hypergeometric distribution

I was too thick to get scipy's Wallenius implementation running (the
[documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.nchypergeom_wallenius.html)
was mostly confusing, sometimes wrong; meaning of function arguments is not obvious ;
most suspicious, however: the function takes one more arguments than is actually
required). Agner Fog's BiasedUrn package, on the other hand, has excellent
[documentation](https://cran.r-project.org/web/packages/BiasedUrn/BiasedUrn.pdf) (and
accompanying
[theory](https://cran.r-project.org/web/packages/BiasedUrn/vignettes/UrnTheory.pdf)).
Although there's a [python package](https://pypi.org/project/biasedurn/), I was too
thick to get this one working as well, so I had to use Agner's own implementation
written for R. Fortunately there's a way to use the R package in python.

One more thing: By default, the code only supports up to 32 different colors (i.e., the
number of different colored balls in the urn). This can be easily fixed, though, by
changing a constant in the code. Here's the full rundown to get it working:

1. Install R
2. Install a customized BiasedUrn package
    1. [Download](https://cloud.r-project.org/src/contrib/BiasedUrn_2.0.10.tar.gz) the
       BiasedUrn package
    2. Extract the source and change `MAXCOLORS` from `32` to `8192` in
     `BiasedUrn/src/Makevars`
    3. Build (`R CMD build BiasedUrn/`) and install (`R CMD INSTALL BiasedUrn_*.tar.gz`)
     the package
3. Install the `rpy2` python module to bridge between Python and R
