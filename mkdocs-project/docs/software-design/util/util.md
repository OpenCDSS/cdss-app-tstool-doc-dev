# Utility Packages #

* [Introduction](#introduction)
* [Potential Future Changes](#potential-future-changes)

------------------

## Introduction ##

Many utility packages are used to provide general functionality.
See the [cdss-lib-common-java](https://github.com/OpenWaterFoundation/cdss-lib-common-java) repository.
Utility packages are used extensively in TSTool because TSTool includes many features
and implements software to access data from many data sources.

See the README file for the above repository for more information.

## Potential Future Changes ##

Over time, it may be possible to phase out some of this code given that the Java standard
libraries now provide similar functionality in some cases,
and third-party libraries are available.
However, using third-party libraries also increases the necessity to monitor, test, and respond
to changes in those packages.
It is likely that the existing utility libraries will continue to be used as is for some time.
