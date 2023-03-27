# Templates #

*   [Introduction](#itroduction)
*   [Software Design](#software-design)

-----------------

## Introduction ##

Templates are text files that include place-holders that can be substituted for with dynamic data.
For example, a time series product file can include a place-holder for the station identifier,
and the same graph template can be used for many stations.
Templating is a powerful concept that can allow TSTool command files to scale beyond built-in software features.

## Software Design ##

TSTool uses the [Apache Freemarker](https://freemarker.apache.org/) package to implement templates.

The primary use of templates is to support the following features:

*   [`ExpandTemplateFile`](https://opencdss.state.co.us/tstool/latest/doc-user/command-ref/ExpandTemplateFile/ExpandTemplateFile/) command for automation
*   time series product files have built in template functionality

TSTool also supports built-in `${Property}` notation for many commands,
which substitute processor properties.
