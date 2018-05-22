# Tables #

* [Introduction](#introduction)
* [Table Design](#table-design)

-------

## Introduction ##

TSTool provides features to automate processing tabular data and tables are a "first class" data object in TSTool,
managed by the processor.
Tables have identifiers that are used to retrieve and save tables to the processor.

## Table Design ##

Tables use a custom
[`DataTable`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/RTi/Util/Table/DataTable.java)
utility class in the
[`Table`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/RTi/Util/Table) package.
This package was originally developed at a time when third-party table packages were lacking and it would
require some effort to replace the existing code.
Table functionality was originally developed to store spatial data shape attributes and was later
enhanced to support reading data from datastores, Excel files, delimited files, etc.

The [`DataTable`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/RTi/Util/Table/DataTable.java)
code design is fairly simple, consisting of the following:

* List of [`DataTableField`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Table/TableField.java) to provide table column metadata
* List of [`TableRecord`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Table/TableRecord.java) to manage table rows
* Other related classes

Data included in tables are expected to extend from the Java `Object` class and null values are allowed.
The table therefore consists of a list of lists (list of
[`TableRecord`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Table/TableRecord.java),
which is list of column object values).
This design could be optimized but works relatively well.
If memory is an issue, the [`FreeTable`](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/command-ref/FreeTable/FreeTable/)
command can be used.
