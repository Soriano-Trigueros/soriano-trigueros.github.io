---
layout: page
title: Vectorization methods
description: Transforming barcodes into valid inputs for statistics and machine learning
img: assets/img/vect_project.png
importance: 2
category: work
---

Despite having such a variety of applications, the workflow used when working with
persistent homology in TDA is rather homogeneous and can be summarized as follows:
1. We start with a data set, usually some finite metric space.
2. Then, a filtration is defined over such data set.
3. The persistent homology of the filtration is computed, to obtain a barcode.
4. Finally, barcodes are analyzed to extract the conclusions of our study.
However, barcodes are not convinient for statistical tests and machine learning. 

In particular, they lack of some of the properties that vector spaces have, like having an unique mean \[MMH-2011\].
For this reason, barcodes are usually send to a vector space (also denoted topological summaries) before performing such analisis.
These vector representation can contain all the information from the original barcode, e.g. persistence landscapes, or just a part of it, e.g. Betti curves.
The possible tradeoffs between the carried information, complexity, interpretability and interaction with the analysis methods lead to interesting research problems. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/flow.png" title="TDA workflow" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Illustration of the typical workflow when using persistent homology in TDA.
</div>

## Univariate statistical tests

Many times in science, and specially in biology or medicine, we only have a data set of limited size.
When this happens, the most common data analysis methods do not apply, and we cannot even assume our values to follow a concrete statistical distribution.
In such case, univariate non-paramteric statistical tests, like the Mann–Whitney U test, are a commonly used.
In order to study barcodes using these tests, we need to summarize their information with just a number.

### Persistent entropy
Persistent entropy is an example of a function that can be used to obtain a number from a barcode.
It can be seen as the Shannon entropy of the lenght of the bars, and was first introduced in \[CGGJK-2015\] and \[RCMP-2016\].
In the paper [On the stability of persistent entropy and new summary functions for topological data analysis](https://www.sciencedirect.com/science/article/pii/S0031320320303125), we studied its formal properties and proposed how to combine persistent entropy and the betti curve to create a new vectorization method,
the entropy summary function.
There exists implementations of persistent entropy in [gudhi](https://gudhi.inria.fr/python/latest/_modules/gudhi/representations/vector_methods.html#Entropy) and [persim](https://persim.scikit-tda.org/en/latest/reference/stubs/persim.persistent_entropy.html).
I made a [tutorial for gudhi](https://github.com/GUDHI/TDA-tutorial/blob/master/Tuto-GUDHI-persistent-entropy.ipynbexplaining) about how to use persistent entropy in TDA.

### Application to epithelial tissues
We were also interested in studying if TDA could measure the differences between the geometrical and topological organization of planar epithelial tissues.
The available data set was small, between 12 and 20 images per type of tissue so it seemed the right settings for using univariate statistical tests.
For this studied, we considered numbers obtained from persistent entropy, evaluation of tropical polynomials and the norm of persistence landscapes. 
We also used different filtrations based in the contact network of the cells and the relative positions of their centroids.
The results were showed in our publication  [Stable Topological Summaries for Analyzing the Organization of Cells in a Packed Tissue](https://www.mdpi.com/2227-7390/9/15/1723).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/cell-filtration.png" title="TDA workflow" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example of filtration used to calculate persistent homology from an epithelial tissue.
</div>

## TDA in machine learning
There are different ways topological data analysis can contribute to machine learning tasks \[ZKNHRP-2023\].
One of them, if to use TDA to quantify some geometrical/topological aspects of the data set and use the resulting vectors as inputs for machine learning algorithms.
As we explained before, there are many possible vectorization methods.
The aim of our research was to compare a big collection of them in classiffication tasks of different classical data sets.
The results were very surprising, vectors formed by list of numbers obtained from simple methods like mean, variance or persistent entropy were performing better than more sofisticated methods.
The whole analysis can be found in [A Survey of Vectorization Methods in Topological Data Analysis](https://arxiv.org/abs/2212.09703)

## References

\[MMH-2011\]
Y. Mileyko, S. Mukherjee, J. Harer. *Probability measures on the space of persistence diagrams*. Inverse Problems 12, nov 2011. DOI: 10.1088/0266-5611/27/12/124007

\[CGGJK-2015\]
H. Chintakunta, T. Gentimis, R. Gonzalez-Diaz, M.J. Jimenez, H. Krim. *An entropy-based persistence barcode*. Pattern Recognition 48-2, feb 2015. DOI: 10.1016/j.patcog.2014.06.023

\[BPCM-2016\]
M. Rucco, F. Castiglione, E. Merelli, M. Pettini. *Characterisation of the Idiotypic Immune Network Through Persistent Entropy*. Proceedings of ECCS 2014, Springer International Publishing. DOI: 10.1007/978-3-319-29228-1_11.

\[ZKNHRP-2023\]
A.Zia, A. Khamis, J. Nichols, Z. Hayder, V. Rolland, L. Petersson. *Topological Deep Learning: A Review of an Emerging Paradigm*. arXiv:2302.03836, aug 2023.
