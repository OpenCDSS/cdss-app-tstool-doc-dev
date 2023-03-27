# Testing Framework #

One of the major features of TSTool is a built-in testing framework that facilitates testing commands in the full application.
Much of the code **does not** currently use Java unit tests (junit), although such tests could be added.
However, the built-in functional testing framework has proven to be capable of testing the software
by exercising code at multiple levels.
This provides coverage testing of the functionality that users will experience.
See the following for more information.

*   [cdss-app-tstool-test test repository](https://github.com/OpenCDSS/cdss-app-tstool-test)
*   [Quality Control chapter of user documentation](https://opencdss.state.co.us/tstool/latest/doc-user/quality-control/quality-control/)
*   [Development Tasks / Testing](../../dev-tasks/overview.md#testing)

Testing TSTool can be complex, especially when using data from third party databased and web services.
For example, it is often necessary to constrain the period of record for time series queries to a
historical period in which data should not change over time.
However, the testing framework does provide significant features to meet testing requirements.

Ultimately, testing focuses on comparing the current software results to expected results.
The testing framework includes commands to compare files, compare time series, and compare tables.
Using simple formats ensures that the testing framework itself can be robust.
