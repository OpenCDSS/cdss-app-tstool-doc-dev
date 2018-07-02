# TSTool / Development Tasks / Coding #

TSTool is mainly coded in Java, although some third-party libraries use "native" code in C and other languages.
For the most part, TSTool development requires Java skills, including understanding all aspects of the language.
Some TSTool is old (~20 years) and therefore may not have benefited from experience gained over the years.
Some code was also ported from other languages, mainly C and C++ and therefore design does not use as many Java features as it could.
Code could also benefit from newer Java features, such as enumeration and `String.format()` and Java 8 time package,
which were not available originally.
These features are implemented over time in order to simplify code and remove reliance on custom code.
Developers should try to use current Java best practices and migrate old code when possible, without breaking such code.

TSTool does not currently use JUnit for unit testing.
Instead, there is great reliance on a built-in testing framework that allows testing the functional software.
This has proven to be very helpful because it automates testing commands and other features,
which then test much of the underlying code.
Additional use of JUnit tests will be phased in as resources allow.

Code formatting has not been a major effort.  It is recommended that new coding follow existing coding in legacy code.
Format for new code can use the Eclipse defaults.
Reformatting code and enforcing a standard is a lower priority given other backlog.

Package names could also use rework.  The current recommendation is to be as consistent as possible; however, significant
package naming cleanup may occur as the OpenCDSS effort is completed.

TSTool development has primarily occurred on Windows computers and therefore files have
traditionally used Windows end of line.
Very early development used command-line editing (`vim` editor, etc.) and then Eclipse was phased in.
Most code therefore has Windows `CRLF` line endings.
More recently, Git Bash and Cygwin Git have been used at times (for example to edit automated tests).
Consequently, there may be some end of line inconsistency in repository files.
Current repositories use `.gitattributes` with `* text=auto` to specify that repository files should use Linux `LF` line endings
and native operating system line endings in working files.
However, there is potential for confusing and this should be monitored and dealt with if issues arise.
