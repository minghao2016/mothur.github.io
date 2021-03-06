---
title: 'kruskal.wallis'
tags: 'commands'
redirect_from: '/wiki/Kruskal.wallis.html'
---
The **kruskal.wallis** command will find the [Kruskal Wallis one way
analysis of
variance](https://en.wikipedia.org/wiki/Kruskal–Wallis_one-way_analysis_of_variance)
for each OTU. To follow along with this tutorial you can download the
example files.

## Default Setting

The shared and design parameters are required.

    mothur > kruskal.wallis(shared=final.an.shared, design=mouse.sex_time.headers.design)

The final.an.0.03.kruskall\_wallis file will look like:

    OTULabel    KW  Pvalue
    Otu001  0.534545    0.464702
    Otu002  0.0981818   0.754023
    Otu003  6.81818     0.00902344
    Otu004  0.541104    0.461975
    Otu005  0.534545    0.464702
    Otu006  0.0109091   0.916815
    ... 

## Options

### label

The label parameter allows you to select what distance level you would
like. Multiple labels can be separated by dashes.

    mothur > kruskal.wallis(shared=final.an.shared, design=mouse.sex_time.headers.design, label=0.03)

### class

If your design file contains multiple categories, you may select the
category you would like to use. If you do not select a class the first
category will be used.

## Revisions

-   1.32.0 - First Introduced
-   1.40.0 - Speed and memory improvements for shared files.
    [\#357](https://github.com/mothur/mothur/issues/357) ,
    [\#347](https://github.com/mothur/mothur/issues/347)


