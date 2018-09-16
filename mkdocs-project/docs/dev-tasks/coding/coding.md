# TSTool / Development Tasks / Coding #

TSTool is mainly coded in Java, although some third-party libraries use "native" code in C and other languages.
For the most part, TSTool development requires Java skills, including understanding all aspects of the language.
Some TSTool is old (~20 years) and therefore may not have benefited from experience gained over the years.
Some code was also ported from other languages, mainly C and C++ and therefore design does not use as many Java features as it could.

TSTool is designed in a way that isolates users from technology changes - command syntax and datastore configuration is
text-based and straightforward.  Therefore, major changes in TSTool design will mainly impact software developers.
The following are important concepts to understand about coding.

* **Code formatting** - Code formatting has not been a major effort.
Eclipse defaults are typically used and ***Source / Format*** is not typically used.
It is recommended that new coding follow existing coding in legacy code.
Format for new code can use the Eclipse defaults.
Reformatting code and enforcing a standard is a lower priority given other backlog.
Code formatting may be a higher priority in the future as more developers engage.

* **Documenting** - Code should be documented using normal standards.
It is important that data, methods, etc. are documented to capture the current developer's design
vision and to ensure that follow-up developers have good context for troubleshooting and enhancements.
Code this is not documented or documentation that is difficult to understand builds in debt that
is borne by future developers.  See the [Documenting](../documenting/documenting) section.

* **Developer Notes** - Code is never perfect and it is often necessary to include notes for future development.
The following guidelines are recommended, using examples.  The `TODO` and `FIXME` phrases are standard
in Eclipse and some other environments.  Including the author and date provides context
for who to contact and whether addressing an issue has languished.
	+ `TODO smalers 2018-09-14 Note for something to do in the future`
	+ `FIXME smalers 2018-09-14 Need to fix this before the release.

* **End of Line** - TSTool development has primarily occurred on Windows computers and therefore files have
traditionally used Windows end of line.
Very early development used command-line editing (`vim` editor, etc.) and then Eclipse was phased in.
Most code therefore has Windows `CRLF` line endings.
More recently, Git Bash and Cygwin Git have been used at times (for example to edit automated tests).
Consequently, there may be some end of line inconsistency in repository files.
Current repositories use `.gitattributes` with `* text=auto` to specify that repository files should use Linux `LF` line endings
and native operating system line endings in working files.
However, there is potential for confusion and this should be monitored and dealt with if issues arise.

* **Java Core Packages** - Some TSTool code is 20 years old and at that time the Java core language did not have
some features, such as enumeration, `String.format()`, and Java 8 time package,
Consequently, custom code was written and is still in use.
Code should be updated to use Java core packages as resources allow and remove reliance on old custom code.
Developers should try to use current Java best practices and migrate old code when possible, without breaking such code.

* **Package naming** - Package names could also use rework.
The current recommendation is to be as consistent with legacy nameing as possible;
however, significant package naming cleanup may occur as the OpenCDSS effort is completed.
In particular, move away from legacy `RTi` root package and towards `cdss`, etc.
Some code organization could improved with sub-packages.
Again, this is a low priority compared to other work items.

* **Testing** - TSTool does not currently rely on JUnit for unit testing.
Instead, there is great reliance on a built-in [testing framework](../testing/testing) that allows testing the functional software.
This has proven to be very helpful because it automates testing commands and other features,
which then test much of the underlying code.
Additional use of JUnit tests will be phased in as resources allow.
However, unit testing is likely to be more of a priority in libraries.
See the [Testing](../testing/testing) section.
