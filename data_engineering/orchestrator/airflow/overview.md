# What is Airflow

Airflow is an orchestrator used to devlop, schedule and monitor batch-oriented workflows. Airflow workflows are defined
in python serving several purposes:

* Dynamic: Airflow pipelines are configured as Python code, allowing for dynamic pipeline generation.
* Extensible: The Airflow™ framework contains operators to connect with numerous technologies. All Airflow components
  are extensible to easily adjust to your environment.
* Flexible: Workflow parameterization is built-in leveraging the Jinja templating engine.

## Access control in Airflow

Access Control of Airflow Webserver UI is handled by Flask AppBuilder (FAB).

#### Default Roles

Airflow ships with a set of roles by default: Admin, User, Op, Viewer, and Public. By default, only Admin users can
configure/alter permissions for roles.

* Admin: Admin users have all possible permissions, including granting or revoking permissions from other users.
* Public: Public users (anonymous) don’t have any permissions.
* Viewer: Viewer users have limited read permissions.
* User: User users have Viewer permissions plus additional permissions.
* Op: Op users have User permissions plus additional permissions.

#### DAG Level Role

Admin can create a set of roles which are only allowed to view a certain set of DAGs. This is called
DAG level access. Each DAG defined in the DAG model table is treated as a View which has two permissions associated
with it (can_read and can_edit. can_dag_read and can_dag_edit are deprecated since 2.0.0). There is a special view
called DAGs (it was called all_dags in versions 1.10.*) which allows the role to access all the DAGs. The default
Admin, Viewer, User, Op roles can all access DAGs view.

### Permissions

Below are different types of Permissions in Airflow
* Resource-Based permissions
* DAG-level permissions
* 
