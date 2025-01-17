R-package for calculation of the Nature Index.
================
Bård Pedersen
April 21, 2021

# NIcalc

*NIcalc* contains a set of utility functions tailored for working with
the Nature Index for Norway. Functions in *NIcalc* may be used to upload
new and revised data into the Nature Index database, to harvest and
assemble data sets from the database, to use these data sets in
calculations of the Nature Index and similar indices, and to summarize
and visualize the results.

## Documentation

*NIcalc* contains documentation and explanations for all functions
included. There are three vignettes: *NatureIndexCalculation* describes
the mathematical framework for calculating the Nature Index and the
associated terminology, *objectsInNIcalc* describes the S3 classes
defined within *NIcalc*, while *Distributions* describes how one may
interact with the Nature Index database in scripts when uploading new
and revised data.

## Install by:

``` r
devtools::install_github("NINAnor/NIcalc", build_vignettes = T)
```

## The most important functions

The functions *importDatasetApi()*, *assembleNiObject()*,
*calculateIndex()*, *getIndicatorValues()*, *setIndicatorValues()*, and
*writeIndicatorValues()* represent the core of *NIcalc*.

#### Updating the Nature Index database with new data

*getIndicatorValues()*, *setIndicatorValues()*, and
*writeIndicatorValues()* may be used in scripts for updating the NI
database with new or revised measurements. *getIndicatorValues()*
retrieves the current values for a given indicator from the NI database
as an S3 object of class *indicatorData*, *setIndicatorValues()* updates
*indicatorData* objects with new measurements, and
*writeIndicatorValues()* posts objects with updated values to the Nature
Index database.

#### How to calculate the Nature Index

*importDatasetApi()* harvests data sets from the database.
*assembleNiObject()* assembles and structures data into a complete and
consistent data set for calculating the Nature Index. *calculateIndex()*
calculates the Nature Index and similar indices. It produces an
extensive output for each index value to facilitate further analyses of
the results.

An example:

``` r
# Not run: 
# Import data set
amphibiaImport <- NIcalc::importDatasetApi(username = "...",password = "...",
                        eco = NULL, indic = c("Småsalamander","Buttsnutefrosk",
                                              "Storsalamander"),
                        year = c("2010","2014","2019"))
# Assemble
amphibiaInput <- NIcalc::assembleNiObject(inputData = amphibiaImport,
                        predefNIunits = c(allArea = T, parts = T, counties = F),
                        indexType = "thematic")
# Calculate index for amphibians 
amphibiaIndex <- NIcalc::calculateIndex(x = amphibiaInput, nsim = 1000,
                        fids = FALSE, tgroups = FALSE, keys = "ignore",
                        w = 0, awbs = TRUE, awBSunit = "Ferskvann")
```

## Contributing to NIcalc

### Questions

If you have questions regarding *NIcalc* please contact
<bard.pedersen@nina.no>.

### Reporting a bug/error

Bug reports can submitted via email to <bard.pedersen@nina.no> or you
can submit an issue [here](https://github.com/NINAnor/NIcalc/issues)

Please provide a reproducible error so that we can see what went wrong.
[Reprex](https://github.com/tidyverse/reprex) is very helpful in this
regard.

Please tell us what you expected to achieve and what the error message
was.

### Submitting code

Pull requests are the best way to propose changes to the code. To do
this please follow these steps:

  - Fork the repo and create your branch from master. If you’ve added
    code that should be tested, add tests.

  - Create a pull request

  - Add an issue associated with each pull request\!

  - Any contributions you make will be under the same License that
    covers the project. Feel free to contact the maintainers if that’s a
    concern.
