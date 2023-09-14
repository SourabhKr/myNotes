# Generic Topics

## Dataform Access to BigQuery

The access to the BigQuery resources can be granted using the Service Account. The default service account created can be used or a custom account can also be used. Non-default service account can be managed at below levels:

1. At the repository level, to run all workflows in a given repository.
2. Individually for each workflow configuration.

Default and non-default service accounts used in Dataform require the following BigQuery IAM roles to be able to execute workflows in BigQuery:

* BigQuery Data Editor on projects to which Dataform needs both read and write access. They usually include the project hosting your Dataform repository.
* BigQuery Data Viewer on projects to which Dataform needs read only access.
* BigQuery Job User on the project hosting your Dataform repository.
* BigQuery Data Owner if you want to query BigQuery datasets.

To use a non-default service account in Dataform, the default Dataform service account must be able to access the non-default service account. To grant this access, you need to add the default Dataform service account as a principal to the non-default service account with the Service Account Token Creator role(roles/iam.serviceAccountTokenCreator).

