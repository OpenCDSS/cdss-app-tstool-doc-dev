# TSTool / Development Environment / Eclipse Run Script #

It is useful to use a script to start Eclipse so that the correct
Java and Eclipse versions are used.

The `cdss-app-tstool-main` repository `build-util` folder contains scripts to run the correct version of Eclipse,
assuming a standard installation folder.
For example, `run-eclipse-win64.cmd` can be run from a Windows command shell,
and `run-eclipse.bash` can be run from a Linux terminal window.
The script ensures that the proper version of Eclipse and configuration is used.
If necessary, this script can be modified to support different versions of Eclipse and Java or other scripts can be added.

The run script is available for new developers that clone the repository.
Ideally the same script can be used by all developers, or a minimal number of scripts can be created to accommodate 
variations in the development environment.
