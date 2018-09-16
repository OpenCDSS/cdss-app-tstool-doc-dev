# TSTool / Development Tasks / Version Control #

TSTool version control uses Git and GitHub and is consistent with CDSS protocols.

* [Version Control Considerations](#version-control-considerations)
* [Version Control Process](#version-control-process)

See also:

* [CDSS / Learn Git](http://learn.openwaterfoundation.org/cdss-learn-git/) documentation.

-------

## Version Control Considerations ##

Major considerations are:

* **Modularity** - TSTool uses an Eclipse workspace to manage multiple projects, each of which correspond to a Git repository.
Some repositories are used by other software, in which case a separate local copy of the repository is usually made.
In other cases separate repositories are used mainly to separate code that
focuses on specific functionality, such as a datastore for a database or web service.
Many repositories rely on the `cdss-lib-common-java` repository because it contains general code such as `TS` for time series.
* **Git Fluency** - TSTool developers are expected to be fluent with Git and be able to deal with its complexities,
such as end of line issues, branching, merging, and effectively using tools.
If a developer is not capable, they should do more homework to learn Git/GitHub and ask questions of others on the team.
* **Git Best Practices** - Git best practices are implemented as much as possible.
Team members can point out where improvements can be made.
* **Feature Branch Model** - the current practice is to use a feature branch model where the `master` branch
is the long-term branch.  Small branches for bug fixes or new features should be created and testing should occur
to ensure that functionality is correct.
Committers can then merge the feature branch into the `master` branch.
Full tests are run on the master branch before making an official release.
* **Merge Approach** - Merging currently uses `git merge --no-ff branchname` approach (not rebasing) until the team
can evaluate its skills and pros and cons of different approaches.
* **Pull Requests** - Pull requests can be made through GitHub.
However, there is currently no online automated testing (with Travis CI, for example).
Therefore pull requests will be integrated on the local computer and tested.
There are not many contributors to TSTool at the moment and management of component libraries may handle integration and testing differently.
* **Consistent Tools** - Multiple Git client exist including command line tools and tools with user interfaces.
Experience has shown that it is best to use consistent Git environments when working with repositories.
For example, use Git Bash for all work rather than using Cygwin for some repositories because Git Bash better integrates with Windows.
Git Bash can be used with other Git clients such as Eclipse.
Symptoms of inconsistent tools are:
	+ File permissions are inaccurately shown as executable (or not).
	+ Git prints excessive messages about line endings.

## Version Control Process ##

The version control process is as follows:

1. **Use the a feature branch approach.** - The `master` branch should always contain tested software.
Feature branches should be created, worked on, and merged as per the following.
Use the [Testing](../testing/testing) protocols to confirm that software is functioning as expected.
2. **Use GitHub issues** - Bugs and enhancements should be added as GitHub issues.
The issue number should be used in the branch name such as `12-bug-commandname`.
3. **Check Git status** - the main `cdss-app-tstool-main` repository contains `build-util/git-check.sh` script.
Run this script in Git Bash to check the status of all repositories used in TSTool.
The script will detect when someone has made changes to a repository and need pulled or local changes need committed or pushed.
4. **Tag repositories for release** - Because TSTool uses multiple repositories,
it can be difficult to check out a specific version later.
Therefore, all repositories are tagged when a TSTool release occurs.
Use the `build-util/git-tag-all.sh` script, which will will prompt for tag information.
The release is usually coordinated by the lead TSTool developer.
