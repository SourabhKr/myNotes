# Workspace

The isolated development environment called Workspace is used for workflow development.  While creating the development workspace in a new repository for the first time, Dataform asks to initialize the development workspace with a set of configuration files that are required for Dataform to work.

An initialized development workspace contains the following directories and files:

* definitions/: a directory for asset definitions, in Dataform core or JavaScript.
* includes/: an empty directory for scripts and variables that you be reused across the repository.
* dataform.json: the default Dataform configuration file containing the Google Cloud project ID and BigQuery schema to publish assets in.
* package.json: the default Dataform dependencies configuration file with the latest version of @dataform/core. This file can also be used to import additional packages.

