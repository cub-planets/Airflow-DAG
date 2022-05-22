# Airflow-DAG
## Downloading and monitoring images by Airflow/DAG
Apache Airflow is an open-source platform to author, schedule, and monitor workflows.
When workflows are defined as code, they become more maintainable, versionable, testable, and collaborative.
Use Airflow to author workflows as directed acyclic graphs (DAGs) of tasks. The Airflow scheduler executes your tasks on an array of workers while following the specified dependencies. Rich command line utilities make performing complex surgeries on DAGs a snap. The rich user interface makes it easy to visualize pipelines running in production, monitor progress, and troubleshoot issues when needed.
## Table of contents

- Project Focus
- Principles
- Requirements
- Getting started
## Project Focus
Airflow is best thought of as a spider in a web: it sits in the middle of your data processes and coordinates work happening across the different (distributed) systems. As such, Airflow is not a data processing tool in itself, but orchestrates the different components responsible for processing your data in data pipelines.
The Airflow scheduler—Parses DAGs, checks their schedule interval, and (if the DAGs’ schedule has passed) starts scheduling the DAGs’ tasks for execution by passing them to the Airflow workers.  The Airflow workers—Pick up tasks that are scheduled for execution and execute them. As such, the workers are responsible for actually “doing the work.”  The Airflow webserver—Visualizes the DAGs parsed by the scheduler and provides the main interface for users to monitor DAG runs and their results.

## Principles
- Dynamic: Airflow pipelines are configuration as code (Python), allowing for dynamic pipeline generation. This allows for writing code that instantiates pipelines dynamically.
- Extensible: Easily define your own operators, executors and extend the library so that it fits the level of abstraction that suits your environment.
- Elegant: Airflow pipelines are lean and explicit. Parameterizing your scripts is built into the core of Airflow using the powerful Jinja templating engine.
- Scalable: Airflow has a modular architecture and uses a message queue to orchestrate an arbitrary number of workers.
## Requirements
Apache Airflow is tested with:
- Python		
- PostgreSQL
- MySQL	
- SQLite	
- MSSQL	

