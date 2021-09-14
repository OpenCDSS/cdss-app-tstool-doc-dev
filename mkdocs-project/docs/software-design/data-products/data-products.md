# Data Products #

* [Introduction](#introduction)
* [UI Product Generation](#ui-product-generation)
* [Automated Product Generation](#automated-product-generation)
* [TSView Reference and GRTS Package](#tsview-reference-and-grts-package)

-----------------

## Introduction ##

"Data products" are primarily graphical time series products, although additional products could be added, such a maps.
TSTool provides extensive features to automate product generation as images.

## UI Product Generation ##

Time series that are created in the TSTool UI and are listed in the ***Results*** can be graphed by selecting the time series
and using available graph menus.
Initial graphs use extensive defaults to ensure reasonable data products.
The product properties can be further edited by right-clicking on a graph and using the ***Properties*** menu.

## Automated Product Generation ##

The [`ProcessTSProduct`](https://opencdss.state.co.us/tstool/latest/doc-user/command-ref/ProcessTSProduct/ProcessTSProduct/) command
is the primary command used to automate data product creation.

Time series product files (`*.tsp`) are used to describe data products.
These files only store non-default product properties, in order to keep product files short.
The time series data that are used in products are listed using time series identifiers (TSIDs) or alias.
This allows the data to be stored separately from the data products,
which is important because data can be very large.
Data products can also make use of templates by using `${Property}` notation and
FreeMarker templating, as described in the
[`ExpandTemplateFile`](https://opencdss.state.co.us/tstool/latest/doc-user/command-ref/ExpandTemplateFile/ExpandTemplateFile/) command.
The syntax of the product files is described in the next section.

## TSView Reference and GRTS Package ##

Data products are described in the
[TSView Documentation in the User Documentation](https://opencdss.state.co.us/tstool/latest/doc-user/appendix-tsview/tsview/).
Extensive properties are available to describe in text form how to create graphical time series products.
The TSView functionality is provided by the following code:

* [`GRTS`](https://github.com/OpenCDSS/cdss-lib-common-java/tree/master/src/RTi/GRTS) package - graphing for time series
* [`GR`](https://github.com/OpenCDSS/cdss-lib-common-java/tree/master/src/RTi/GR) package - underlying drawing library

The above libraries were developed at a time when other alternatives were not available.
These packages are integrated with the core time series package to provide optimized graphing.
Performance is very good.
Some users may prefer to use Excel for charting
However, TSTool provides features such as zooming and paging/scrolling that are not available in Excel.
