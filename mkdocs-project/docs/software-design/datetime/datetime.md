# Date/time Handling #

* [Introduction](#introduction)
* [DateTime Class / Java Date / Java 8 `java.time` Package](#datetime-class-java-date-java-8-javatime-package)
* [Instantaneous and Interval-ending Data Values](#instantaneous-and-interval-ending-data-values)
* [0 and 24 Hour Clocks](#0-and-24-hour-clocks)
* [Time Series Interval Bins](#time-series-interval-bins)
* [Time Zone](#time-zone)

----------------

## Introduction ##

Date/time handling is critical to properly handling time series and other time-stamped data.

## DateTime Class / Java Date / Java 8 `java.time` Package ##

The Java [Date](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html) class and related classes have been available in Java since early releases.
However, there are well-known issues with this class that can make it almost impossible to write good functional code.

Java 8 included the new [java.time](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html) package,
which provides a significant enhancements and resolves issues with the legacy `Date` class.
Even so, it is important to understand how to use the new package, and it will take time to transition from legacy Java `Date` class to new `java.time` package.
Developers are encouraged to use `java.time` where it makes sense and phase out use of Java `Date` class; however, read the remainder of this page first.

Because the built-in Java `Date` class was insufficient, the "home grown"
[`DateTime`](https://github.com/OpenWaterFoundation/cdss-lib-common-java/blob/master/src/RTi/Util/Time/DateTime.java) class was created for use in TSTool.
This class has the following characteristics:

* Internally represents data using date/time parts (year, month number, day number, etc.).
It does not use an internal long integer such as Unix Epoch (time since Jan 1, 1970) to represent time, as some libraries do,
although it has methods to convert to and from long integers, based on Java `Date`.
Conversion between `DateTime` and other date/time representations will continue to evolve as Java 8 `java.time` is integrated.
* Recognizes a precision internally, for example to ensure that date/time only includes hour, but not minute and second.
The precision is consistent with time series interval.
The `toString()` method therefore can automatically format a `DateTime` to the proper precision.
* Provides methods to parse and format date/time strings.
* Provides methods to increment/decrement time, including `addInterval()` that is compatible with `TS` data interval, used for iteration.
* Is aware of time zone as a string, with some support for conversions.
This is an area that can be further enhanced with Java 8 `java.time` package features.
* `DateTime` are mutable.  This functionality was chosen by design to support efficient time series processing without
having to create date/time object instances for each time series timestep.
Features are built into `TS` and other classes to create a copy of the `DateTime` to protect against unexpected modification to objects by reference.

**Does it make sense to replace `DateTime` with `java.time` classes?** Perhaps, but there is so much code that this will take awhile.
It does make sense to phase `java.time` in as a replacement for legacy Java `Date` and related classes.
However, there are many considerations related to legacy code, such as SQL database specification and drivers that use `Date` and have not been
updated to use `java.time`.
Once a critical mass of code has been transitioned to `java.time`, then an evaluation of totally phasing out `DateTime` can occur.

## Instantaneous and Interval-ending Data Values ##

Data values, such as those within time series, have a date/time and corresponding value.
The interpretation of the date/time depends on the data type and its recording method.
Some time series contain original values and other time series contain calculated values.

Instantaneous values have date/time that closely matches the observation time, for example stream water level or flow.
Instantaneous observation time may be irregular such as when an event occurs,
or may be scheduled to align with time boundaries such as minute 00, 15, 30, 45.

Statistical values are typically calculated based on interval, such as accumulation, difference, minimum, maximum, or mean value.
For example, instantaneous streamflow values in a 60-minute interval might be averaged to calculate a 1-hour mean flow value.
Or, precipitation increments in a 15-minute interval might be totaled to give the 15-minute rain total.

Within TSTool and other tools, it is common that the date/time for calculated values corresponds to the interval-ending time.
For example, the mean streamflow recorded at date/time `YYYY-MM-DD 12:00:000` corresponds to the mean of 15-minute values at minute 15, 30, 45, and 00.
When visualized, such as using a bar chart, or a line that draws horizontally until the value changes, it is clear that the mean
value applies during the indicated interval.
However, different tools may handle calculations differently.
Software developers and users must understand how data are recorded.

Within TSTool, interval data are referred to as regular time series, and data reported at irregular times are referred to as irregular time series.

## 0 and 24 Hour Clocks ##

Time series in TSTool internally use 0-hour clock, meaning that there is not an hour 24 in the day.
A time of HH:MM 23:59 plus one minute is 00:00 of the next day.
This can cause issues with some calculations and data visualization, in particular for hourly data.
For example, 1-hour mean value data for a day will have times
01, 02, 03, 04, 05, 06, 07, 08, 09, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, and 00 (of next day).
It is particularly confusing when using 24-hour time series with `HourTS` class, where interval base is hour and multiplier is 24.
In this case, it is often easier to understand if the time series is treated as a time series with interval 1Day or Day.

## Time Series Interval Bins ##

Time series arrays in TSTool are configured for fast date/time lookup.
For example, a `MonthTS` time series for monthly data is organized as a two-dimensional array with year as one index and month as the other.
This results in a "binning" of data that works as long as there are no time offsets.
For example, requesting any value from a monthly time series using a `DateTime` object that has daily precision will return
the same monthly value because the daily value is "binned" within the same month.

Hourly data are a bit more challenging due to time zones with daylight savings, operational situations where data span multiple time zones,
and schedules that do not align with nice intervals.  For example, a 6-Hour time series might align with hour 7 in an operational system because the location
is in a time zone that is 7 hours offset from GMT.  In this case the 6-Hour data are recorded at hours 01, 07, 13, and 19.
TSTool's data arrays are allocated based on the data interval and align with hours 00, 06, 12, and 18.
In this example, integer math internally results in truncation that stores the values in the proper "bin".
The perhaps unanticipated result of this is that a request for data using an hour anywhere within the bin will return the value assigned to that bin,
rather than missing value.
This issue is typically not a major problem because most time series align at interval boundaries or are instantaneous.
However, inconsistencies can occur if code does not properly consider the offset
and mixing time series intervals in calculations.
In the future, a flag may be added to `TS.getDataValue()` method such as `requireExactAlignment`.

## Time Zone ##

Handling time zone is one of the trickier aspects of data management and time series.
TSTool does not perform on-the-fly time zone conversions and relies on a few conventions.

Time zone is represented in databases, files, and web services using a time zone number or string.
Time zones can change based on location, time of year (daylight savings),
and policy or legislative changes such as have occurred historically in various states and territories.
Time zones associated with times for data values are typically represented in local time or standard time.
If standard time, the time zone does not change throughout the year.
For example, "MST" corresponds to Mountain Standard Time, which is always offset by -7 hours from UTC.
However, "MDT" corresponds to Mountain Daylight Time, which is offset by -6 hours from UTC.
Daylight saving shift occurs once in the fall (fall back), in which case the data record will have one value overwritten at 2:00 AM on the designated day,
and once in the spring (spring forward), in which case the data record will be missing one interval at 2:00 AM on the designated day.

* See:  [Daylight saving time in the United States on Wikipedia](https://en.wikipedia.org/wiki/Daylight_saving_time_in_the_United_States)

TSTool for the most part does not care about time zone, especially if all data are within an area where time zone is consistent.
However, time zone is important to display data so that data users understand time for data values.
Consequently, TSTool will save the time zone in `DateTime` when read from input.
In order to ensure consistent handling of data, TSTool generally will not automatically shift data.
For example, if the time zone is local time, the date/time values are parsed as is, resulting a gap of one value each spring.
The main issue occurs with regular time series because the start date/time is used to display output or write date/times to files.
If the time zone associated with data changes throughout the year but only the time zone for start is saved,
then the time zone used for display may be wrong at certain times of the year.
This issue has become more of a problem with the use of [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) time zone notation
and implementation in software.
For example, data from a web service might be returned as follows, assuming instantaneous values:

```text
125,840,840,"2018-03-11T00:00:00-07:00",91.0
125,840,840,"2018-03-11T01:00:00-06:00",91.5
125,840,840,"2018-03-11T03:00:00-06:00",92.0
125,840,840,"2018-03-11T04:00:00-06:00",93.0
125,840,840,"2018-03-11T05:00:00-06:00",96.0
```

In the above, values were observed at midnight and 1AM as usual.  However, when the value was observed at 2AM, daylight savings was implemented and "spring forward" by an hour occurred.
Consequently, there was no actual 2AM on the clock and therefore the value was recorded at 3AM.
Alternatively, the system could have recorded a 2AM value and 3AM might have been missing for the next recording.
Anyone using the data must know that the data are recorded in local time and must be willing to deal with the single missing value every year.

The bigger issue for TSTool is that the time zone changed from `07:00` to `-06:00`.
For regular-interval time series, TSTool code will output the start `DateTime` time zone for the entire period.
Consequently, part of the year will be displayed (or will be output) with time zone that is one hour offset.
This will result in misinterpretation and other software that reads the data will introduce additional errors.
In this specific case, the following can be done:

1. Shift the date/time for each data value to the time zone corresponding to the start `DateTime`.
	* This is bad because the `DateTime` internal data will no longer match the source.
	* This is bad because data users will probably be confused, during part of the year.
2. Remove the time zone (set to blank string).
	* This is bad because then the time has no time zone and could lead to confusion (although local time is often assumed as a default).
3. Change the time zone string to something more general that is constant throughout the year, such as "America/Denver",
	which is technically correct.
	* This is OK but requires software features to change the time zone.
	* This is bad if the time series is output and third-party software cannot handle the time zone
	(but can handle the original source -07:00 and -06:00).
4. Enhance TSTool design to allow time zone string to change within the year.

Option 2 is perhaps the best option to avoid erroneous output.
Option 3 is perhaps the next best if software can be updated.
Option 4 will take more time to evaluate.
Note that this is only an issue with time series that have hour or minute data interval.
