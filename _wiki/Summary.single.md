---
title: 'Summary.single'
---
The [summary.single](summary.single) command will produce a
summary file that has the calculator value for each line in the OTU data
and for all possible comparisons between the different groups in the
group file. This can be useful if you aren\'t interested in generating
collector\'s or rarefaction curves for your multi-sample data analysis.
It would be worth your while, however, to look at the collector\'s
curves for the calculators you are interested in to determine how
sensitive the values are to sampling. If the values are not sensitive to
sampling, then you can trust the values. Otherwise, you need to keep
sampling. For this tutorial you should download and decompress
[AmazonData.zip](Media:AmazonData.zip)


### Default settings

Enter either of the following commands:

    mothur > summary.single(list=98_lt_phylip_amazon.fn.list)

or to run the single analysis with multiple samples:

    mothur > make.shared(list=98_lt_phylip_amazon.fn.list, group=amazon.groups)
    mothur > summary.single(shared=98_lt_phylip_amazon.fn.shared)

The summary data for all of the single sample
[calculators](calculators) is generated by default with the
following command:

    mothur > summary.single(list=98_lt_phylip_amazon.fn.list)

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
the right column indicates the row number in the data set. In dotur, the
summary data was provided in separate files ending in \"ltt\" and was
only generated after the collector\'s curves were generated. Now, in
mothur, all of this data is contained within a single \"summary\" file.
In this case data was written to the file
98\_lt\_phylip\_amazon.fn.summary, which looks like:

    label  Sobs        Chao        Chao_lci    Chao_hci
    unique 96.000000   1558.222222 347.616318  8593.437067
    0.00   95.000000   1144.375000 350.293575  4408.417964
    0.01   93.000000   732.222222  307.998499  1993.501867
    0.02   89.000000   1255.666667 288.403803  6914.903478
    0.03   84.000000   481.193878  227.569853  1182.858662
    0.04   81.000000   315.945000  179.197207  643.125486
    0.05   73.000000   179.211735  119.908132  313.489912
    0.06   68.000000   143.306667  100.656145  241.660852
    0.07   66.000000   121.723183  90.116038   194.755526
    0.08   59.000000   92.109568   72.389087   140.875896
    0.09   57.000000   96.744444   72.675322   157.771188
    0.10   55.000000   95.158163   70.499679   159.045903

Again, the first column contains the label for the row in the data set
you are analyzing. Next, the first row of each column is labeled to
indicate the calculator that was used to generate the data. For
instance, here the data in the column labeled Sobs contains the number
of OTUs that were observed in each row of the data set. Next in this
file are the data for the Chao1 richness estimator. Because there are
formulae for the 95% confidence intervals the first column contains the
actual estimator and the next two columns contain the value for the
lower and upper bound on the interval.

## Options

### calc

If you don\'t want to see all of the default calculators, you can tell
mothur which ones to use in the summary file:

    mothur > summary.single(list=98_lt_phylip_amazon.fn.list, calc=sobs-chao-npshannon)

This would generate the 98\_lt\_phylip\_amazon.fn.summary file:

    label  Sobs        Chao        Chao_lci    Chao_hci    NPShannon
    unique 96.000000   1558.22222  347.61631   8593.43706  7.768419
    0.00   95.000000   1144.37500  350.29357   4408.41796  7.355786
    0.01   93.000000   732.222222  307.99849   1993.50186  6.831284
    0.02   89.000000   1255.66666  288.40380   6914.90347  6.344819
    0.03   84.000000   481.193878  227.56985   1182.85866  5.800593
    0.04   81.000000   315.945000  179.19720   643.125486  5.559488
    0.05   73.000000   179.211735  119.90813   313.489912  5.090494
    0.06   68.000000   143.306667  100.65614   241.660852  4.853388
    0.07   66.000000   121.723183  90.116038   194.755526  4.776910
    0.08   59.000000   98.4453120  74.865828   157.068166  4.483528
    0.09   57.000000   105.568047  75.830083   182.270567  4.377893
    0.10   55.000000   100.872781  72.625547   174.389885  4.286385

### abund

By default the [ACE estimator](ACE_estimator) uses 10 as the
cutoff between OTUs that are rare and abundant. So if an OTU has more
than 10 individuals in it, then it is considered abundant. This is
really just an empirical decision and we are merely following the lead
of Anne Chao and others who implement 10 in their software. If you would
like to use a different cutoff, you can use the abund option:

    mothur > summary.single(calc=ace, abund=5)

Looking at the file, 98\_lt\_phylip\_amazon.fn.summary, you\'ll see that
when the distance is 0.10, the ACE estimate value is 101.1 (95%
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
interested in summarizing. There are two options. You could: (i)
manually delete the lines you aren\'t interested in from you rabund,
sabund, or list file; (ii) or use the label option. To use the label
option with either the summary.single() command you need to know the
labels you are interested in. If you want the summary data for the lines
labeled unique, 0.03, 0.05 and 0.10 you would enter:

    mothur > summary.single(list=98_lt_phylip_amazon.fn.list, label=unique-0.03-0.05-0.10, calc=sobs-chao)

Opening 98\_lt\_phylip\_amazon.fn.summary you would see the output as:

    label  Sobs        Chao        Chao_lci    Chao_hci
    unique 96.000000   1558.22222  347.616318  8593.437067
    0.03   84.000000   481.193878  227.569853  1182.858662
    0.05   73.000000   179.211735  119.908132  313.4899120
    0.10   55.000000   100.872781  72.6255470  174.3898850

### groupmode

If you are running summary.single with a shared file and would like your
summary results collated in multiple files, set groupmode=f.
(Default=True). If you run:

    mothur > make.shared(list=98_lt_phylip_amazon.fn.list, group=amazon.groups)
    mothur > summary.single(shared=98_lt_phylip_amazon.fn.shared, groupmode=t)

    label  group   sobs    chao    chao_lci    chao_hci ...    
    unique forest  48.000000   588.500000  235.495870  1606.115657 ...     
    unique pasture 48.000000   588.500000  235.495870  1606.115657 ...     
    0.00   forest  48.000000   588.500000  235.495870  1606.115657 ...     
    0.00   pasture 48.000000   588.500000  235.495870  1606.115657 ... 
    0.01   forest  47.000000   377.000000  165.127879  968.882296 ...      
    0.01   pasture 47.000000   377.000000  165.127879  968.882296 ...  
    0.02   forest  46.000000   519.000000  208.687352  1421.208320 ... 
    0.02   pasture 44.000000   905.000000  517.445731  1609.799312 ...     
    0.03   forest  45.000000   332.000000  146.710970  854.833987 ...      
    0.03   pasture 43.000000   433.000000  175.375225  1192.006545 ... 
    0.04   forest  44.000000   239.000000  115.962675  572.398926 ...      
    0.04   pasture 43.000000   433.000000  175.375225  1192.006545 ...

### subsample

The subsample parameter allows you to enter the size of the sample or
you can set subsample=T and mothur will use the size of your smallest
group in the case of a shared file. With a list, sabund or rabund file
you must provide a subsample size.

### iters

The iters parameter allows you to choose the number of times you would
like to run the subsample. Default=1000.

### withreplacement

The withreplacement parameter allows you to indicate you want to
subsample your data allowing for the same read to be included multiple
times. Default=f.

## Revisions

-   1.29.0 Added subsample options.
-   1.40.0 - Speed and memory improvements for shared files.
    [\#357](https://github.com/mothur/mothur/issues/357) ,
    [\#347](https://github.com/mothur/mothur/issues/347)
-   1.40.0 - Fixes segfault error for commands that use subsampling.
    [\#357](https://github.com/mothur/mothur/issues/357) ,
    [\#347](https://github.com/mothur/mothur/issues/347)
-   1.42.0 - Adds withreplacement parameter to sub.sample command.
    [\#262](https://github.com/mothur/mothur/issues/262)
-   1.43.0 - Modifies output files from dist.shared, summary.single and
    summary.shared. You may run with or without rarefaction, but not
    both. [\#607](https://github.com/mothur/mothur/issues/607)

[Category:Commands](Category:Commands)