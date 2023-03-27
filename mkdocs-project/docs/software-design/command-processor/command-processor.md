# Command Processor #

*   [Introduction](#introduction)
*   [Processor Properties](#processor-properties)
*   [Processor Data](#processor-data)
*   [Communicating with Processor](#communicating-with-processor)

-------------

## Introduction ##

The [TSCommandProcessor](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java)
class (generically referred to as "command processor" or "processor")
is the core class that handles processing commands shown in the TSTool UI and
when processing command files in batch mode.
For historical reasons, there are two main classes,
which may be combined into a single class in the future:

*   [TSEngine](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java) - original processor class
*   [TSCommandProcessor](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java) - modern command processor, calls TSEngine

The current design maintains most large [processor data](#processor-data) in the 
[TSCommandProcessor](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java) class,
whereas [processor properties](procesor-properties) are split between the processor and the
[TSEngine](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java) instance used by the processor.
[TSEngine](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java) functions
are called from the processor to perform work.
Some conventions that are in place were implemented many years ago and will require resources to change and test.
For example interactive processing requests (graphs, reports) that originate in the UI are requested from the
[TSEngine](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java) class.
In general, code should interact with the
[TSCommandProcessor](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSCommandProcessor.java) class,
which wraps
[TSEngine](https://github.com/OpenCDSS/cdss-lib-processor-ts-java/blob/master/src/rti/tscommandprocessor/core/TSEngine.java).
 
## Processor Properties ##

Properties are maintained in the processor to control processing.
Properties fall into two categories:

*   "built-in properties" have meaning to the core processor/engine and are defined with built-in data members.
    For example, the global output period start and end.
    Built-in properties are generally objects, not primitives, in order to better handle missing/null.
*   "user-defined properties" provide flexibility for controlling workflows via `${Property}` notation.
    User-defined properties are first-class objects, not primitives:

```
/**
HashMap of properties used by the processor.
HashMap allows null keys and values, although here keys should be non-null.
*/
private HashMap<String,Object> __propertyHashmap = new HashMap<String,Object>();
```

The unique identifier for a property is its property name.
Internal code to get and set properties uses the property name to determine whether a property is built-in or dynamic,
and performs the appropriate action.

The following are complexities with properties:

*   **How to handle missing/null** - properties that are not defined will have a value of null if requested.
    Missing values are generally treated similarly.
    String values should distinctly handle differences between null/missing and spaces.
    Calling code must handle the difference between missing/null and empty strings.
*   **How to handle case-specificity** - TSTool code is generally forgiving related to case-specificity
    but does try to enforce standards.
    The default is to use property names that are `MixedCase`.
    However, to minimize issues with case, much of the code compares strings by ignoring case.
    This protocol was implemented early on due to Microsoft operating systems generally not enforcing case.
    This approach can be problematic with properties because internally the HashMap is case-specific.
    The general trend in TSTool is to move towards case-specificity for properties,
    although the code works well now so major changes are not envisioned.

## Processor Data ##

The processor maintains lists of objects including time series, tables, and datastores, for example:

```
/**
List of DataTable objects maintained by the processor.
*/
List<DataTable> __TableList = new Vector<DataTable>();
```

Classes that are maintained in this way are required to have an "ID" data member that identifies instances of the object.
For time series this is the "TSID" and the alias can also be used.
Tables and other objects have simple identifier string.
The identifier is used by commands run by the processor to request objects to process, and the identifier
is used by the UI to display and access results.

Time series identifiers are not required to be unique.
This derives from historical design decisions, for example where a time series is read multiple times and
one is modified and compared to the original.
This is one reason why time series commands use the `TSList` parameter to specify how to select the time series to process.

The general design approach is to add lists of major data objects as the processor is enhanced,
and use properties for configuration and processing control.
With this approach, the core processor can be kept conceptually simple.

## Communicating with Processor ##

The processor performs many tasks, which requires corresponding internal methods.
Commands have a reference to the processor that is used to process the command.
The TSTool UI maintains an instance of a processor to process commands.
However, providing access to a processor with many methods increases difficulty in maintaining the processor
and all code that calls the processor.
Exposing the large number of methods could lead to code that is difficult to maintain.
Consequently, a "service" approach was taken in the design, whereby a general `processRequest()` method
is called with a request method name and list of parameter objects to the method.
Private internal methods such as `processRequest_IndexOf` are then used to perform the task and return the results.
This design was also initially chosen to allow for the possibility of distributed processing
where the processing requests could occur on one computer and the processing could occur on another computer
(this functionality has never been implemented).
After having used this approach, it would be possible to evaluate the design and use an alternative approach if
resources are available.
