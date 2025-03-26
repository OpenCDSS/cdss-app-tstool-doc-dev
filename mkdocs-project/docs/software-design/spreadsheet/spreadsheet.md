# TSTool / Software Design / Spreadsheet #

*   [Introduction](#introduction)
*   [Spreadsheet Code Design](#spreadsheet-code-design)

---------

## Introduction ##

Spreadsheet support was added to TSTool after table features were implemented.
Excel workbooks can represent tabular data in worksheets.
Users also prefer to provide workflow input as Excel and create Excel output products.
TSTool does not provide ability to fully automate reading and writing all Excel features;
however, the commands that are provided have been used effectively to process large datasets.

## Spreadsheet Code Design ##

Spreadsheet code uses the [Apache POI](https://poi.apache.org/) library, which reads and writes Microsoft documents including
Word and Excel files.
The library is quite extensive and as is the case with Apache libraries relies on Apache components.

Handling Excel files is tricky, especially when reading, because the data lives in two locations, the Excel file, and
the in-memory representation of the Excel file.
TSTool commands use a "keep open" concept when an Excel file should be kept open between commands
because otherwise the Excel file might be rewritten with partial contents.
There are also complexities to deal with related to mapping Java object types to Excel,
dealing with missing data, formulas, etc.
