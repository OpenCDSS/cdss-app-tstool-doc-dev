# Commands that Read Time Series #

* [Introduction](#introduction)
* [`readTimeSeries` Method](#readtimeseries-method)
* [`readTimeSeriesList` Method](#readtimeserieslist-method)
* [Typical Read Command Logic](#typical-read-command-logic)
* [Date/time Handling](#datetime-handling)

----

## Introduction ##

This documentation focuses on the design and implementation of commands that read time series.
Such code is typically implemented by using a low-level input/output data management interface (DMI) library
that is called by command code or main TSTool UI code.
Time series reading is initiated by the following cases:

1. **Data Browsing** - Read partial time series via the TSTool main UI in order to populate the time series list at the top of the TSTool main UI.
In this case, the `readTimeSeries` method for a datastore (database or web service) or input type (often a file type)
is called with the `readData=false` method parameter.
The time series (`TS`) object will be created and most of the properties can be set.
However, reading time series data and filling the data arrays will be skipped.
This form of the time series is useful within TSTool and command processor to allow editing commands that need time series
information such as TSIDs and aliases.

2. **TSID Command** - Read time series via the command processor (run via UI or command line) by processing a TSID command,
which is a line in a command file with only a TSID.
The TSID is an "implicit read" in that it cases a `readTimeSeries` method to be called
on the matching datastore or input type, using the identifier after the `~` in the TSID.
Because the TSID is a simple string with no command parameters, the read uses default values:
	1. The default input period is used (from datastore defaults or global input period).
	2. Alias may be assigned using default values.

3. **Generic Read Command** - Read time series via the command processor (run via UI or command line) by processing a `ReadTimeSeries` or `ReadTimeSeriesList` command.
These commands allow for more control during the read than a simple `TSID` command.
However, the read is still fairly generic given that only generic command parameters can be specified, such as:
	1. Assign alias.
	2. Allow period of record to be specified.

4. **Specific Read Commands** - Read time series via the command processor (run via UI or command line) by processing read commands that
have been specifically written for a data source.
These commands provide the greatest control over the read process, for example:
	1. Provide input parameters to help select time series in cases where TSID is complex.
	2. Read multiple time series and provide filters to control which time series are read.
	3. Assign alias.
	4. Allow period of record to be specified.
	5. Internally, assign time series properties such as station or site properties.

## `readTimeSeries` Method ##

Each class that provides functionality to read time series, such as a datastore or file reader class,
should provide a `readTimeSeries` method to read a single time series, with at least the following parameters.
**This is not currently an interface but is likely to be so in the future.**

```
readTimeSeries(String tsid, DateTime readStart, DateTime readEnd, boolean readData )
```

A summary of the parameters is given in the following table.  See also [Date/time Handling](#datetime-handling).

|**Parameter**|**Description**|**Default if null**|
|--|--|--|
|`tsid`|Time series identifier string that follows general guidelines but parts have specific meaning for the datastore, file, etc.  For example, the datatype may contain sub-parts to allow reading the data.| None - must be specified. |
|`readStart`|The `DateTime` to start reading.  If not specified to a precision corresponding to the data interval, suitable handling must occur.  The DateTime instances that are saved in the time series object will be truncated to the precision of the time series data interval. Irregular time series may save full DateTime precision.|Depends on the datastore, but typically will cause the entire period to be read, or in some cases for real-time data, a short recent period.  TSTool tends to show as much data as possible and then users can shorten the period as they prefer to study a part of the period of record or to improve performance.|
|`readEnd`|Similar to `readStart`| Similar to `readStart`.|
|`readData`|The purpose of this parameter and associated functionality is to provide the option of reading time series metadata (hopefully fast), and also allow reading entire time series data values (which may be slow).  If `false`, then the time series will be created and as many properties as possible will be read and assigned internally.  If `true`, then the time series data array will also be read and set in the time series.|No default since primitive type.  For example, `false` is used when reading the time series to display in the TSTool browse area and `true` is used when processing time series in the command processor.|

Some code also includes a `units` parameter to indicate that data units should be converted to those indicated.
However, this functionality is not uniformly implemented because units abbreviations and names are not consistent.
Instead, the TSTool `ConvertDataUnits` or `Scale` commands can be used after reading the time series.

## `readTimeSeriesList` Method ##

Some datastores allow reading multiple time series via a `readTimeSeriesList` method.
This functionality has been added over time, in particular for commands that provide query filters similar
to the main TSTool UI (for example, see `ReadHydroBase` command).

A typical design is to implement a method that has multiple query parameters consistent with the datastore.
For example, some datastores may allow filtering locations by county or geographic coordinates.
The logic is typically:

1. Request the list of stations or time series metadata using query/filter parameters.
2. For each object returned from the above, read the specific time series using `readTimeSeries`
described in the previous section.

In some cases, the `readTimeSeriesList` command may not call `readTimeSeries`,
such as when a web service API bundles multiple time series together in a result and/or requesting time series one by one
will result in significantly slower performance.

## Typical Read Command Logic ##

This section focuses on `readTimeSeries` method, although the logic would be similar for `readTimeSeries`.
Developers should review existing datastore code for examples of how to implement new code.

The logic to read time series via a `readTimeSeries` method varies depending on input format.
For example, a file format may dictate how data are read and used because data in the file are provided in a specific order.
In contrast, databases or web services may require multiple requests to be made to retrieve all necessary data,
and may use internally cached objects to improve performance when multiple time series are read.
Although the order of logic may change, the following steps generally occur:

### 1. Parse the time series identifier (TSID) that was passed to the `readTimeSeries` command.

The parts of the TSID provide a unique "address" for the time series and provide the fundamental information
necessary to locate the time series source and read the time series from that source.
The following TSID parts are typically the most fundamental to reading time series:

* Input type part of the TSID after the `~` at the end indicates the datastore or input type code class to use.
This information also will have been used by calling code to determine what classes to use to read the time series.
	+ If a datastore is used, then the processor will maintain a list of datastores that can be accessed by the command.
	Access to database and web service resources will occur via the datastore object.
	+ If an input type is used (see main TSTool UI for list of input types),
	then the input is either a file, or an older database connection that
	has not been converted to a datastore (although an effort has been made to convert to new datastore design).
	If a file, then the TSID indicates the input file after a second `~`, as in `~StateMod~PathToFile`.
	Filenames that are relative path are converted to absolute path based on command file location.
* Time series interval is used to determine what time series class to instantiate, such as `DayTS`, `MonthTS`, etc.
* Time series data type is used to determine what database tables or web services to query.
Very seldom does a database or web service provide exactly what is needed in one request.

Other parts of the TSID, such as the location ID, are used for specific queries and are discussed below.

### 2. Create the Time Series Object ###

The interval (time step) from the TSID is used to create an instance of the correct time series object.
The interval may be indicated in various ways in the original data source, for example:

1. "daily", "day", "d" or some other indicator may be used for daily data
2. "inst", "instantaneous", "random", "realtime", "sparse", or other indicator may be used for real-time data

The above variation causes issues with consistency. Therefore, within TSTool and associated code,
intervals are always converted to general form (e.g., TSTool uses "Day" instead of "Daily"),
and a numerical value is used internally (not yet a true Java enumeration but similar).
TSTool is generally case-independent to allow flexibility and therefore "Day" and "day" are equivalent.

TSTool and library code have traditionally used the general "irreg" or "irregular" to indicate irregular-interval data.
This worked for many years.
However, more recently there has been a need to understand precision for irregular time series,
for example to know that some daily data are recorded only infrequently.
Consequently, effort is underway to introduce intervals like "irregday".
These features will be phased in over time.

To facilitate time series creation, use the [`TSUtil.newTimeSeries`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSUtil.java) method,
which handles many interval strings and returns an empty instance of `DayTS`, `MonthTS`, etc.
Note that this method does not call `setTimeSeriesIdentiifer` method on the instance so
call after the time series is returned.

### 3. Set Core Time Series Properties ###

Core time series properties are used by TSTool and other code and should always be set if possible.
The data from input may require querying other data, such as stations.
Some core data are maintained in the TSID via the `TSIdentifier` class, with `TS` methods that chain to `TSIdentifer` methods.

* Identifier - required to identify the time series
	+ `TS.setIdentifier()` - usually called immediately after `TSUtil.newTimeSeries()` is called to create the time series.
* Description - helpful to understand time series contents
	+ The time series description (sometimes called name) is a short phrase that describes time series.
	The description from orginal source or as constructed by TSTool is often a combination
	of location and data type, for example `ABC River at City, streamflow`.
	Consequently, it may necessary to read location data (see next section) to createa a suitable description.
	+ `TS.setDescription()` - sets the description
* Data Interval (time setep) - required for data management, access, iteration
	+ The interval base and multipler are maintained in the `TSIdentifier` instance so don't need to call anything else.
	+ The interval is often needed for processing later and get methods are provided.
* Period of record - used to allocate memory arrays and for information
	+ See also the [Date/time Handling](#datetime-handling) section.
	+ `TS.setDate1()` - set the starting DateTime for in-memory data array
		- If a requested start was provided, use it because that is what the calling code requested
		- The DateTime may need to be rounded to ensure alignment with data
		(e.g., convert a current date/time to 15-minute if that is what the data use).
		Rounding is typically to an earlier date/time for start, and to a later date/time for end.
	+ `TS.setDate2()` - set the ending DateTime for in-memory data array, similar to start
	+ `TS.setDate1Original()` and `TS.setDate2Original()`
		- Set to the original data limits if available, for example the full period in a database or file.
		- If unknown, set to the same values used with `setDate1()` and `setDate2()`.
	+ DateTime in TS objects will automatically have precision set to the interval of the time series when the above methods are called.
	+ Note that the TS class set methods make copies of DateTime since they are mutable and need to prevent against accidental changes.
	In particular `TSIterator` and for loops over DateTime need to be isolated from changing internal TS DateTime instances.
	+ Setting the period does not automatically allocate memory for the time series data.
	The `TS.hasData()` method can be called later to check whether data arrays have been defined,
	and calls to `TS.getDataValue()` will return the missing value if data have not been read.
* Data units - required to properly interpret data
	+ `TS.setDataUnits()` - set the current units.
	+ `TS.setDataUnitsOriginal()` - set the original units, can be the same as current units
* Missing value - required to handle missing valus
	+ The missing value is a special numerical value that indicates missing data (no value available).
	`null` cannot be used because the data array uses primitive `double` to save memory.
	Older code used `-999.0` for missing value because the United States Geological Survey used.
	Newwer code uses `NaN` (not a number).
	+ `TS.setMissing()` and `TS.setMissingRange()` can be used to set the missing value.

### 4. Set Additional Time Series Properties ###

Additional time series properties can be set and are often related to secondary data.
For example, time series internal data fundamentally do not involve location other than for identification part of TSID. 
However, location type and information are often needed to streamline data processing,
such as processing all time series in a county or river basin.
The following are addtional time series properties that can be set at initialization and during later processing:

* Time series history - used to explain data processing
	+ `TS.addToGenesis()` - add a message to explain reading data, for example `"Read data from web service theURL"`.
* Time series comments - used to pass on comments from original source
	+ `TS.addToComments()` - for example, may contain narrative about station history
* Data flag metadata - used to explain data flags
	+ `TS.addDataFlagMetadata()` is used to add a description for data flag metadata
	+ Data flags are used by some time series and typically consist of a single character to explain data, such as `e` for estimated.
	The data flag array will be allocated automatically when setting a data flag,
	assuming that the start and end for the main data array have been set.
	+ The data flag metadata is used in output products, such as graph legends.
* Selected - used to interact with TSTool
	+ `TS.setSelected()` - is used with interactive results selection, `SelectTimeSeries()`, and `DeselectTimeSeries()` commands.
	Commands that have `TSList` parameter check the selection to know whether to process time series.
	+ Generally not called by read code.
* Enabled - used in special cases such as when graphing time series and want to disable
	+ `TS.setEnabled()` - generally not called by read commands
* General properties - add any free-form properties
	+ A general hash map of properties is kept and can be displayed in TSTool by right-clicking on a time series in results and
	selecting ***Time Series Properties***.  Some output formats will also handle, such as DateValue files.
	+ `TS.setProperty()` sets a property.
	+ To retain as much original data as possible, the data values from associated location (station, site, etc.) should be set as properties.
	This also allows those properties to be used in workflows, sich as by using `SetPropertyFromTimeSeries` command.

### 5. Read Time Series ###

If the `readTimeSeries` or `readTimeSeriesList` method is called with `readData=true`, times series data values will be read.
The first step is to allocate the time series memory based on the requested input period:

* `TS.allocateDataSpace()` - allocates the data array and initializes with missing data value.
**Need to call this automatically when data values are set.**
* `TS.allocateDataFlagSpace()` - allocates the data flag array, in cases where data flags are used.
Newer code automatically calls as needed when data are set.

Looping through data in the source format then should then extract date/time, values, and flags.
The `DateTime` class is designed to re-use an instance (is not immutable).
Therefore, when looping through data, it is possible to reuse a DateTime instance.
Otherwise, rely on `DateTime.parse()` to parse a string.

Setting data in `IrregularTS` provide the option of setting a duration.  Set the duration to zero or -1 if not valid.
The duration is sometimes used to indicate a span over which the irregular time series value was measured,
since there is no regular interval to indicate this information.

### 6. Additional Processing in Command ###

Additional processing may occur in the command for time series that are read, not the `readTimeSeries` method, for example:

1. **Assign the alias**.  This may occur in the command because the original time series code and APIs did
not include passing the alias string to read methods and because there can be some complexity when time series properties
are used to dynamically set the alias.
The alias is sometimes set in the read method, in particular when the command processes multiple time series.
2. **Set time series in processor.**  Once time series are read, the are added to the list of time series maintained
by the processor.

## Date/time Handling ##

Date/time handling is critical to implementing commands that read time series.
See the general discussion of [Date/time Handling](../datetime/datetime).
