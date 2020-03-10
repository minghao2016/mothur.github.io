---
title: 'Collect.single'
---
[collect.single](collect.single) generates collector\'s
curves using [calculators](calculators), that describe the
richness, diversity, and other features of individual samples.
Collector\'s curves describe how richness or diversity change as you
sample additional individuals. If a collector\'s curve becomes parallel
to the x-axis, you can be reasonably confident that you have done a good
job of sampling and can trust the last value in the curve. Otherwise,
you need to keep sampling. For this tutorial you should download and
decompress [AmazonData.zip](Media:AmazonData.zip)


## Default settings

By default, the collect.single() command will randomize the order in
which the individuals are sampled. So if you run collect.single()
multiple times, you will get slightly different results. The
collector\'s curve data for all of the [single sample
calculators](single_sample_calculators) is generated by
default with the following command:

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list)

This will result in output to the screen looking like:

    unique 1
    0.00   2
    0.01   3
    0.02   4
    0.03   5
    0.04   6
    0.05   7
    0.06   8
    0.07   9
    0.08   10
    0.09   11
    0.10   12

The left column indicates the label for each line in the data set and
the right column indicates the row number in the data set. Execution of
collect.single() will generate 8 files, one for each of the richness and
diversity calculators. If you look at 98\_sq\_phylip\_amazon.fn.sobs you
will see something like:

    numsequences   unique  0.00    0.01    0.02    0.03    0.04    0.05    0.06    0.07    0.08    0.09    0.10
    1      1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000
    98     96.0000 95.0000 93.0000 89.0000 84.0000 81.0000 73.0000 68.0000 66.0000 59.0000 57.0000 55.0000

In this file the first column tells you how many sequences have been
sampled; this would typically be plotted on the x-axis of a graph. Each
subsequent column has a heading, which indicates the label for the line
being analyzed from your OTU data file. The data in the column tells you
how many OTUs were observed for that label and number of sequences. By
default, collect.single() prints output every 100 sequences.

For some calculators there are formulae that enable us to determine the
95% confidence intervals. For example, if you look at
98\_sq\_phylip\_amazon.fn.chao, you will see something like:

    numsampled unique  lci hci 0.00    lci hci 0.01    lci hci 0.02    lci hci 
    1      1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000  1.5000
    98     1558.2  347.61  8593.4  1144.3  350.29  4408.4  732.22  308.00  1993.5  1255.7  288.40  6914.9

Again the first column tells you how many sequences have been sampled.
You then need to look at the columns in groups of three. The first
column of the set of three has a heading, which indicates the label for
the line being analyzed from your OTU data file. The data in the column
tells you how many OTUs were predicted, using the Chao1 estimator, to be
in that sample for that label and number of sequences. The following two
columns contain the bounds on the 95% confidence interval.

To run the single analysis with multiple samples:

    mothur > make.shared(list=98_lt_phylip_amazon.fn.list, group=amazon.groups)
    mothur > collect.single(shared=98_lt_phylip_amazon.fn.shared)

## Options

### calc

If you are not interested in producing collector\'s curves for all of
the calculators, it is possible to select the calculators you want using
the calc option:

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list, calc=sobs-chao)

This command would only generate the files
98\_lt\_phylip\_amazon.fn.sobs and 98\_lt\_phylip\_amazon.fn.chao. Note
that the sobs file does not have 95% confidence intervals where as the
chao file does.

### abund

By default the [ACE estimator](ACE_estimator) uses 10 as the
cutoff between OTUs that are rare and abundant. So if an OTU has more
than 10 individuals in it, then it is considered abundant. This is
really just an empirical decision and we are merely following the lead
of Anne Chao and others who implement 10 in their software. If you would
like to use a different cutoff, you can use the abund option:

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list, calc=ace, abund=5)

Looking at the file, 98\_lt\_phylip\_amazon.fn.collect, you\'ll see that
when the distance is 0.10, the final ACE estimate value is 101.1 (95%
CI=75.5-158.8) compared to 161.4 (95% CI=120.3-228.4) when abund was 10.
You will not see a difference when the maximum abundance is below the
threshold.

### size

Within the suite of calculators available in mothur are a set that will
predict the [number of additional
OTUs](Calculators#Estimates_of_number_of_additional_OTUs_observed_with_extra_sampling)
that will be observed for a given sample size. By default these
calculators will base the prediction on a sample that is the same size
as the initial sampling. If you would like to use a different sample
size, use the size option:

    mothur > summary.single(list=98_lt_phylip_amazon.fn.list, calc=boneh, size=50)

The value of size should be between 1 and the size of the initial
sampling. If you go beyond those limits, the default sample size will be
used.

### label

There may only be a couple of lines in your OTU data that you are
interested in generating collector\'s curves for. There are two options.
You could: (i) manually delete the lines you aren\'t interested in from
you rabund, sabund, or list file; (ii) or use the label option. To use
the label option with the collect.single() command you need to know the
labels you are interested in. If you want the collector\'s curve data
for the lines labeled unique, 0.03, 0.05 and 0.10 you would enter:

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list, label=unique-0.03-0.05-0.10)

In the file 98\_sq\_phylip\_amazon.fn.sobs you would see something like:

    numsequences   unique  0.03    0.05    0.10
    1      1.0000  1.0000  1.0000  1.0000
    98     96.0000 84.0000 73.0000 55.0000

### freq

For larger datasets you might not be interested in obtaining all of the
data for the number of sequences sampled. For instance, if you have
100,000 sequences, you may only want to output the data every 100
sequences. Alternatively, if you only have 100 sequences, you may only
want to output all of the data. The default setting is to output data
every 100 sequences. By altering the freq option you can set the
frequency that the analysis is performed:

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list, freq=1)

or

    mothur > collect.single(list=98_lt_phylip_amazon.fn.list, freq=10)

or you set set the frequency as a percentage of the number of sequences.
For example to output after 25%:

     mothur > collect.single(list=98_lt_phylip_amazon.fn.list, freq=0.25)

The second command would generate data such as this:

    numsequences   unique  0.00    0.01    0.02    0.03    0.04    0.05    0.06    0.07    0.08    0.09    0.10
    1      1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000  1.0000
    10     10.0000 10.0000 10.0000 10.0000 10.0000 9.0000  9.0000  10.0000 9.0000  8.0000  10.0000 9.0000
    20     20.0000 19.0000 20.0000 19.0000 20.0000 19.0000 17.0000 20.0000 19.0000 15.0000 18.0000 19.0000
    30     30.0000 29.0000 29.0000 29.0000 29.0000 29.0000 25.0000 28.0000 27.0000 21.0000 25.0000 25.0000
    ...

## Revisions

-   1.40.0 - Speed and memory improvements for shared files.
    [\#357](https://github.com/mothur/mothur/issues/357) ,
    [\#347](https://github.com/mothur/mothur/issues/347)

[Category:Commands](Category:Commands)