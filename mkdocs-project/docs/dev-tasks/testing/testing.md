# TSTool / Development Tasks / Testing #

* [Unit Testing](#unit-testing)
* [Functional Testing](#functional-testing)

------------------

## Unit Testing ##

TSTool does not currently use JUnit for unit testing because the functional testing framework allows testing the full stack of software.
However, JUnit may be used more in the future, especially for library components that do not have a clear functional test.
The `test/` folder in each repository can be used for unit tests, other than the `cdss-app-tstool-test` folder includes functional tests.

## Functional Testing ##

TSTool testing relies on extensive functional tests.

* See the [cdss-app-tstool-test test repository](https://github.com/OpenWaterFoundation/cdss-app-tstool-test)
* See the [Quality Control](http://learn.openwaterfoundation.org/cdss-app-tstool-doc-user/quality-control/quality-control/)
chapter of the TSTool user documentation.

Functional testing typically occurs in a granular fashion by adding and running tests for specific commands.
Prior to software release, the full suite of tests is run by running the following command files in the
`cdss-app-tstool-repository`:

1. Run `test/regression/TestSuites/commands_general/create/Create_RunTestSuite_comands_general_IncludeOS=Windows.TSTool`.
This searches all the command tests and creates a command file with `RunCommands` commands for each command.
2. Run `test/regression/TestSuites/commands_general/run/RunRegressionTest_commands_general_IncludeOS=Windows.TSTool`.
This runs the tests in the previous item.
Some tests historically fail and need to be dealt with to ensure 100% pass.
