# TSTool / Development Tasks / Troubleshooting Eclipse #

Some of the common Eclipse issues are:

1.  **Class not found** - Make sure that the build path is correct, which sets the Java classpath to include
    other projects in the workspace and specific jar files.
    If the build path is correct, then using a new class in a source file should allow right-clicking and adding the corresponding import statement.
2.  **Refresh code** - If any operations are done outside of Eclipse, such as using Git command line tools or adding/editing files,
    then make sure to refresh the project of interest by right-clicking on the project name and selecting ***Refresh*** or ***F5***.
3.  **Many code warnings** - Eclipse provides many warnings, some of which may be difficult to understand.
    Many remaining warnings in TSTool code are related to the need to implement generics convention,
    for example to convert `List a` to `List<String> a`.
    This is generalized simple to do for simple code but can be complex when class inheritance and other design issues are more complex.
    Developers should make an attempt to address warnings but need to be careful not to introduce side-effects.
    In many cases it may be appropriate to insert an annotation to ignore the warning, such as when a cast is really required.
