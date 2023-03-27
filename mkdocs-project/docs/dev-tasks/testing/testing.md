# TSTool / Development Tasks / Testing #

*   [Unit Testing](#unit-testing)
*   [Functional Testing](#functional-testing)

------------------

## Unit Testing ##

TSTool does not currently use JUnit for unit testing because the functional testing framework allows testing the full stack of software.
However, JUnit may be used more in the future, especially for library components that do not have a clear functional test.
The `test/` folder in each repository can be used for unit tests, other than the `cdss-app-tstool-test` folder includes functional tests.

## Functional Testing ##

Functional tests are those that exercise the software under operational use cases.
The term "end to end testing" may also be used.
TSTool testing relies on extensive functional tests.

*   See the [cdss-app-tstool-test test repository](https://github.com/OpenCDSS/cdss-app-tstool-test)
*   See the [Quality Control](https://opencdss.state.co.us/tstool/latest/doc-user/quality-control/quality-control/)
    chapter of the TSTool user documentation.

Functional testing typically occurs in a granular fashion by adding and running tests for specific commands.
Prior to software release, the full suite of tests is run by running the following command files in the
`cdss-app-tstool-repository`:

1.  Run `test/test-suites/commands-general/create/Create_RunTestSuite_comands_general_Windows.tstool`.
    This searches all the command tests and creates a command file with `RunCommands` commands for each command.
2.  Run `test/test-suites/commands-general/run/RunRegressionTest_commands_general_Windows.tstool`.
    This runs the tests in the previous item.
    Some tests historically fail and need to be dealt with to ensure 100% pass.

Use the output files that are created by TSTool (listed in the ***Results*** area) to review test results.
Fix tests that do not pass, either by changing the software or adjusting the test.
