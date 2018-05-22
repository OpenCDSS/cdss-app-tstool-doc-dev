# Time Series #

* [Introduction](#introduction)
* [Time Series Concepts](#time-series-concepts)
* [Time Series Identifier and Alias](#time-series-identifier-and-alias)
* [Time Zone Handling](#time-zone-handling)
* [Time Series Classes](#time-series-classes)
* [Time Series Iteration](#time-series-iteration)
* [Time Series Utility Classes](#time-series-utility-classes)

-----------

## Introduction ##

TSTool was originally developed primarily as a time series processor and this remains as one of its primary functions.
This documentation discusses time series concepts and code that relates to time series.

## Time Series Concepts ##

Time series concepts related to TSTool are discussed in the
[TSTool Introduction in the User Documentation](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/introduction/introduction/).

### Time Series Data Values ###

Time series in basic form consist of a data "array":

* date or date/time, also sometimes called timestamp - instantaneous or interval-end
* value - the data value, typically a number
* data flag - a string indicating data quality, etc.

Although it is possible to store multiple data values at a date/time,
this causes issues with identifying and manipulating the data in a general way.
Instead, a basic convention is that only one data type (value) can be stored in a time series.
Time series can be grouped for reading/writing, such as writing multiple time series for a station to a delimited file.

Time series values can be stored in "regular" interval time series, meaning that the date/time are evenly separated,
such as every 15 minutes.
Or, time series values can be stored in "irregular" interval, meaning that the date/time can be any time.
Regular interval time series are easier to process and data storage can be optimized because date/time only needs
to be stored at the period start and end (although see [Time Zone Handling](#time-zone-handling) for issues).

### Data Flags ###

Time series are designed to support granular data flagging for each data value.
No standard flag values are required because data from various sources have their own flag conventions.
In many cases, a single-character flag will be used, such as `m` for missing or `e` for estimated.
However, in other cases, multiple-character flags may be used.
Therefore, the time series design allows multi-character flags.

Many commands that set or fill time series values allow a flag to be specified.
An enhancement in recent years has been to allow the flag value to indicate whether
the flag should be reset, appended to, etc.
Additional work will occur in this area.

Time series also include [TSDataFlagMetadata](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSDataFlagMetadata.java) to describe data flags.
The metadata is output in some formats such as
[DateValue](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/datastore-ref/DateValue/DateValue/).

### Time Series Properties ###

In addition to the data, properties are also needed to fully manage the time series.
The following are major properties:

* Identifying Information
	+ Location type - The location type is an optional property that is useful
	when location types might be confused, for example city and county of Denver.
	+ Location - Although TSTool typically is used for processing data associated with stations (or sites), 
	the concept of location can be generalized to sensor, area, political unit, etc.
	The location is typically a station or other location identifier.
	+ Data source - TSTool internally uses a data source to indicate originating entity, such as government agency.
	+ Data type - The data type is typically a short string, such as "precip", but can be a numerical code or composite value.
	+ Interval - string version corresponding to interval below,
	indicates the spacing of data values, where [N] is assumed to be equivalent to 1 if not specified
		- [N]Minute
		- [N]Hour
		- Day
		- Month
		- Year
	+ Scenario - optional scenario indicator
	+ Sequence (trace) ID - optional sequence identifier, typically year of trace in an ensemble
* Period
	+ Start
	+ End
	+ Original start - prior to extending/truncating, or available in original source
	+ Original End - prior to extending/truncating, or available in original source
* Interval - internal representation in
[TimeInterval class](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/TimeInterval.java)
	+ Base interval
	+ Interval multiplier
	+ Base interval, original - before conversion
	+ Interval multiplier, original - before conversion
* Units
	+ Units
	+ Original units - prior to a conversion
* Missing value
	+ Internally a range to handle numerical round-off for values like `-999`
	+ `NaN` also recognized
* Data limits
	+ Useful to summarize data
	+ Base class that is extended for monthly limits
	+ Primarily used for monthly limits based on historical requirements
* Descriptive information
	+ Description
	+ Genesis history (how modified)
	+ Comments
	+ Properties - free-form property=value properties
* Data flags
	+ Additional data array
	+ Metadata - used to describe flag values

## Time Series Identifier and Alias ##

Internally, time series are retrieved using a time series identifier (TSID),
that is a dot-delimited string comprised of optional location, data source, data type, interval, and optional scenario.
Additionally a leading `locationType:` and trailing `[trace]` can be included.
The TSID is used by commands to retrieve time series and add new time series.
Because the TSID can be cumbersome, time series also support the use of an alias, which can be any string.
A request to find matching time series for processing will check the alias first and then TSID.
The [TSIdent](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSIdent.java) class is used to store and manipulate TSIDs.

The [TSTool Introduction in the User Documentation](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/introduction/introduction/)
discusses TSIDs and aliases.
TSIDs and aliases are very important and are used in displays, logging, and nearly all functionality.

## Time Zone Handling ##

Properly handling time zones is important for time series with data interval hour and minute,
and irregular time series with date/times that are hour or minute precision.
Day, month, and year interval time series generally do not use time zone.

### DateTime Class ###

The [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java) class
was developed specifically to support time series.
Early Java date/time classes such as
[`Date`](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html) have well-known limitations including
being cumbersome to work with.
The new [Java 8 time package](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html) address many limitations;
however, TSTool would require extensive upgrades to fully use this package.
The new package is being phased in where it makes sense,
but third-party packages vary in their use, in particular database libraries.

The custom [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java) class
provides a number of features that work well with time series including:

* Mutable
	- In particular for time series iterators the
	[`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java)
	instance can be incremented or decremented by the time series interval.
	Mutable design is not always desirable but it helps with performance in this case
	**Perhaps need to implement an ImmutableDateTime class**.
* Time zone is handled as much as needed but does not overwhelm (see more discussion below).
* No limit on internal representation since milliseconds, UNIX epoch, or other datum is not used.
* Performance of the class has been demonstrated.

Time zone is stored in [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java)
as a simple string, mainly used for comparison and output/display.
Where additional conversion is needed, the time zone is converted to number.

### Time Zone in Start and End DateTime ###

One of the main issues related to time zone is its use in specifying the data period.
Regular interval time series only store the start and end date/time and time zone needs to be consistent,
in order to avoid offset issues.
Time zones can be specified in date/time string in several ways:

1. Time zone is constant across year:
	1. Time zone is standard time:
		1. GMT
		2. MST
		3. -07:00 (offset from GMT)
		4. etc.
		5. No daylight saving changes
	2. Time zone is local time:
		1. `America/Denver`
		2. `Mountain`
		3. etc.
		4. Daylight saving changes so in spring will have missing value when spring forward
		and in fall a value will be lost because a value is overwritten
2. Time zone changes during full year:
	1. Daylight saving string:
		1. `MST` and `MDT` (seems to be less common and out of favor)
		2. [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) `-07:00` and `-06:00` depending on time of year

Within TSTool, the first option is OK given that the numerical 
[`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java) values
will be OK if used as is.
Case 1.1 is consistent because time zone is consistently a standard zone with no daylight savings changes.
Case 2.1 is consistent because although daylight savings occurs, the time zone name remains constant and time is consistent with the time zone.
The biggest issue is case 2.x because the time zone string changes during the year and if the start and end
[`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java) in the
time series have different time zone string, confusion will result.
Consequently, time series need to generate an error when:

* start and end date/time have different time zone
* a date/time is used to set data and the time zone for that date/time is different from the start
	+ could allow an alternate time zone to be used or changing time zone ignored,
	but in any case the time zone would need to be consistent

Consistency can be enforced mainly by handling time zone when reading and writing time series.
Once the time series is in memory, the time zone is generally ignored except for printing.
The ISO-8601 offset from GMT is clear, but it causes issues using the data when time zone changes,
therefore, it may be necessary to request an override when read into TSTool, such as convert to standard time zone that does not vary,
convert to a local time zone, etc.

## Time Series Classes ##

TSTool relies heavily on the [TS package](https://github.com/OpenWaterFoundation/cdss-lib-common-java/tree/master/src/RTi/TS)
Significant effort has gone into designing the classes in this package to handle regular and irregular interval time series
in an efficient way.
The Java TS package is based on earlier C and C++ versions and still retain some design elements from those languages,
such as relying on inheritance rather than interfaces to define behavior.
Based on requirements, separate time series classes were written for each distinct data interval, as listed below.

|**Interval**|**Time Series Class**|
|--|--|
|NSecond|Not yet supported, but can use [`IrregularTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/IrregularTS.java)|
|NMinute|[`MinuteTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/MinuteTS.java)|
|NHour|[`HourTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/HourTS.java)|
|Day|[`DayTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/DayTS.java)|
|Week|Not yet supported, but can use [`IrregularTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/IrregularTS.java)|
|Month|[`MonthTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/MonthTS.java)|
|Year|[`YearTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/YearTS.java)|
|Irregular|[`IrregularTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/IrregularTS.java)|

The above classes have distinct approaches for managing data values arrays,
depending on the precision of the interval.
For example, the [`YearTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/YearTS.java) class
stores a one-dimensional array of values, whereas 
[`MinuteTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/MinuteTS.java) uses a three-dimensional array.
Data array index lookups are performed using date/time parts.
This is different than using, for example, millisecond equivalent of date/time in a linear array.
Experience has shown that the time series as implemented are very fast.

One intricacy in the design is that each array index for storing data is assumed to behave well for the interval.
For example, for monthly regular interval time series, each slot aligns with a month number.
However, some data, in particular NHour data, such as 6Hour data, can be tricky.
For example, a time series may be described as having 6Hour interval but data values are stored at hour 1, 7, 13, and 19
due to time zone alignment.
Integer math used to determine indices will generally work OK as in the first index will match hours ending 1-6, the second 7-12,
the third 12-18, and the fourth 19-0 (or 19-24).
However, time zone inconsistencies may cause a shift in the slot and lookups will not be correct.
An enhancement in the future may be to include more checks for alignment.
This is not generally an issue but can be in some cases.  See also [Time Zone Handling](#time-zone-handling).

Similarly, year interval data may correspond to calendar or other year types.
The year type is not currently saved in the time series.

The time series classes have arrays for `double` values and `String` flags.
This allows `Double.NaN` or a double value to be used for missing value.
String data flags use "interned" strings, meaning that reusing a flag value will reuse the same string.
Time series only use strings when flags are needed, thereby saving memory.
Currently, there is no way to store an `int`, a `String`, or other data type in time series,
unless new classes such as `StringMinuteTS` were implemented.
There are some exceptions, such as 
[`StringMonthTS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/StringMonthTS.java),
which is used to store monthly Wet/Dry/Average indicators for data filling.
A decision was made not to treat the data value as abstract `Object` type,
in order to save memory and because there was no requirement for such design at the time.

## Time Series Iteration ##

Time series are commonly iterated for input, output, analysis, and visualization.
Consequently, there is a need for efficient iteration design.
There are two main ways to iterate over time series data.

1. Simple for/while loop.
	1. Start with time series start [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java).
	2. End with time series end [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java).
	3. Increment the [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java)
	by calling [`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java)
	`addInterval()` method matching time series interval base and multiplier.
	4. Retrieve data values using
	[`TS`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TS.java)
	`getDataValue()` or similar method.
2. Iterator class.
	1. Call the time series class `iterator()` function to create a
	[`TSIterator`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSIterator.java) instance.
	If an irregular time series, a
	[`IrregularTSIterator`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/IrregularTSIterator.java) will be returned.
	2. Use the iterator methods to advance the date/time and retrieve corresponding data values via
	[`TSData`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSData.java) objects.

The second approach is approved for new code and should be phased in given that it
uses a consistent approach.

In either case, care should be taken to use
[DateTime](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java)
objects that align with the time series.
This can be tricky because a requested processing interval may use date/times that are in different precision or may be offset from even intervals.
Time series processing code deals with such issues.

The iterators are optimized.
For example, the [`IrregularTSIterator`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/IrregularTSIterator.java)
remembers the last request and is able to quickly retrieve the next or previous value.

## Time Series Utility Classes ##

Numerous tasks need to be performed on time series, such as filling missing data, converting the data to a one-dimensional array, etc.
Rather than bloat the time series classes with extensive methods, utility classes are provided with static methods.
Initially, the [`TSUtil`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSUtil.java) class contained all such methods.
However, this class was becoming very long.
Consequently, recent code changes have migrated utility code into separate classes with `TSUtil_` name,
such as [`TSUtil_SortTimeSeries`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/TS/TSUtil_SortTimeSeries.java).
These classes can be used as needed.
Often, a utility class matches a TSTool command, where the command provides a parameter-based command
for workflow processing and the utility class provides the computational functionality.
