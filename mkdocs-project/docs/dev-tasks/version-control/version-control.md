## TSTool / Development Tasks / Version Control ##

TSTool version control uses Git and GitHub and is consistent with CDSS protocols.

* See the [CDSS / Learn Git](http://learn.openwaterfoundation.org/cdss-learn-git/) documentation.

Major considerations are:

1. **Modularity** - TSTool uses an Eclipse workspace to manage multiple projects, each of which correspond to a Git repository.
Some repositories are used by other software, in which case a separate local copy of the repository is usually made.
In other cases separate repositories are used mainly to separate code that
focuses on specific functionality, such as a datastore for a database or web service.
Many repositories rely on the `cdss-lib-common-java` repository because it contains general code such as `TS` for time series.
2. **Git Fluency** - TSTool developers are expected to be fluent with Git and be able to deal with its complexities,
such as end of line issues, branching, merging, and effectively using tools.
If a developer is not capable, they should do more homework to learn Git/GitHub and ask questions of others on the team.
3. **Git Best Practices** - Git best practices are implemented as much as possible.
Team members can point out where improvements can be made.
4. **Feature Branch Model** - the current practice is to use a feature branch model where the `master` branch
is the long-term branch.  Small branches for bug fixes or new features should be created and testing should occur
to ensure that functionality is correct.
Committers can then merge the feature branch into the `master` branch.
Full tests are run on the master branch before making an official release.
5. **Merge Approach** - Merging currently uses `git merge --no-ff branchname` approach (not rebasing) until the team
can evaluate its skills and pros and cons of different approaches.
6. **Pull Requests** - Pull requests can be made through GitHub.
However, there is currently no online automated testing (with Travis CI, for example).
Therefore pull requests will be integrated on the local computer and tested.
There are not many contributors to TSTool at the moment and management of component libraries may handle integration and testing differently.
