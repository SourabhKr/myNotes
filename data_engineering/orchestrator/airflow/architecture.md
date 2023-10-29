# Airflow Architecture

Core components that make up Airflow are:

* Scheduler: A scheduler, which handles both triggering scheduled workflows, and submitting Tasks to the executor to
  run.
* Executor: An executor, which handles running tasks. In the default Airflow installation, this runs everything inside
  the scheduler, but most production-suitable executors actually push task execution out to workers.
* Webserver: A webserver, which presents a handy user interface to inspect, trigger and debug the behaviour of DAGs and
  tasks.
* Folder of Daf Files: A folder of DAG files, read by the scheduler and executor (and any workers the executor has)
* Metadata database: A metadata database, used by the scheduler, executor and webserver to store state.

![overall_architecture](/asset/images/airflow/architecture.png)

_Airflow itself is agnostic to what you’re running - it will happily orchestrate and run anything, either with
high-level
support from one of our providers, or directly as a command using the shell or Python Operators._

## Workloads

Workloads are nothing but DAGs in Airflow, and each DAG can contain multiple tasks, which are individual jobs that needs
to be performed.

Tasks are of basically below type:

* Operators: predefined tasks that can be stringed together.
* Sensors: a special subclass of Operators which are entirely about waiting for an external event to happen
* A TaskFlow-decorated @task: which is a custom Python function packaged up as a Task.

Internally, these are all actually subclasses of Airflow’s BaseOperator, and the concepts of Task and Operator are
somewhat interchangeable, but it’s useful to think of them as separate concepts - essentially, Operators and Sensors are
templates, and when they are called in a DAG file, they are essentially making a Task.

## Control Flow

DAGs are designed to be run many times, and multiple runs of them can happen in parallel. DAGs are parameterized, always
including an interval they are “running for” (the data interval), but with other optional parameters as well.

Tasks have dependencies declared on each other. You’ll see this in a DAG either using the >> and << operators
Or, with the set_upstream and set_downstream methods:

```python
first_task.set_downstream([second_task, third_task])
third_task.set_upstream(fourth_task)
```
