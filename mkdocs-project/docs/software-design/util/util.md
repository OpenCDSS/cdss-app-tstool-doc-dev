# Utility Packages #

*   [Introduction](#introduction)
*   [Potential Future Changes](#potential-future-changes)

------------------

## Introduction ##

Many utility packages are used to provide general functionality.
See the [cdss-lib-common-java](https://github.com/OpenCDSS/cdss-lib-common-java) repository.
Utility packages are used extensively in TSTool because TSTool includes many features
and implements software to access data from many data sources.

See the README file for the above repository for more information.

## Potential Future Changes ##

Over time, it may be possible to phase out some of this code given that the Java standard
libraries now provide similar functionality in some cases,
and third-party libraries are available.
For example the [`StringUtil.formatString()`](https://github.com/OpenCDSS/cdss-lib-common-java/blob/master/src/RTi/Util/String/StringUtil.java)
method can be replaced with Java's
built-in [`String.format()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) method.
Many of the "home grown" features were developed because no equivalent was available
at the time and there has been no reason to change the code.
However, using third-party libraries also increases the necessity to monitor, test, and respond
to changes in those packages.
It is likely that the existing utility libraries will continue to be used as is for some time.
