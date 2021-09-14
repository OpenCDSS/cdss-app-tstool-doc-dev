# TSTool / Development Environment / Git #

* [Install Git Software](#install-git-software)
* [Git Issues to be Aware of](#git-issues-to-be-aware-of)

---------------

## Install Git Software ##

Install Git command line or other tools.

Git/GitHub are used for version control.
It is expected that developers are proficient with Git and will configure and use a familiar Git client, such as:

* Git within Eclipse
	+ **Developers should confirm handling of end of line in Eclipse version that is
	being used - repositories now have `.gitattributes` with `* text=auto`.**
* Git for Windows:  Git Bash or Git GUI
* Git features in text editor
* GitHub Desktop
* Cygwin git command line (**only use for repositories that are cloned with Cygwin Git**)
* Other Git client

See also [CDSS / Learn Git](https://opencdss.state.co.us/cdss-learn-git/).

## Git Issues to be Aware of ##

Each Git client implements defaults that are used when cloning and working with a repository and there are some important
issues to be aware of, which can vary by repository:

* **End of line character** - use of `.gitattributes` with `* text=auto` stores newline in the repository and uses operating system
end of line in working files (`CRNL` for Windows and `NL` for Linux).
This is needed to avoid situation where developers in different environments "flip-flop" the end of line character on commits.
It may be necessary at some point to confirm that line endings in the repository are the generalized newline because `CRNL`
may have been committed previously.  Text editors have ways to show end of line character.
* **File permissions** - Git only stores file permission as file mode `100644` (not executable) or `100755` (executable).
Tools such as screen capture software may cause the permissions to be wrong.
Avoid issues by using Git client that is consistent with how the clone occurred (do not mix Cygwin wit Windows git clients).
Use the GitHub blame tool to view permissions and watch for the file mode in git command line messages, such as `git commit`.
* **Ignore case** - Git Windows clients often configure defaults to ignore case in Windows environments,
which may allow some issues to occur, such as typos in filenames that need to be case-specific.
Developers need to be aware.

Git configuration properties for software and repository can be viewed using:

```
git config --list --show-origin
```
